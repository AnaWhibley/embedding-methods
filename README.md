import { BehaviorSubject } from 'rxjs';

export abstract class BaseRegistry<T> {
  private subject?: BehaviorSubject<T>;

  add(value: T, substitute: boolean = true): void {
    if (this.subject && !substitute) return;
    if (this.subject) this.subject.complete();

    this.subject = new BehaviorSubject(value);
  }

  get(): BehaviorSubject<T> | undefined {
    return this.subject;
  }

  update(value: T): void {
    if (!this.subject) throw new Error(`[${this.getRegistryName()}] No subject`);
    this.subject.next(value);
  }

  destroy(): void {
    if (this.subject) {
      this.subject.complete();
      this.subject = undefined;
    }
  }

  abstract getRegistryName(): string;
}

export class ChartScopedRegistries {
  private registries = new Map<string, BaseRegistry<any>>();

  constructor(registryFactories: Record<string, () => BaseRegistry<any>>) {
    for (const [name, factory] of Object.entries(registryFactories)) {
      this.registries.set(name, factory());
    }
  }

  getRegistry<T extends BaseRegistry<any>>(name: string): T | undefined {
    return this.registries.get(name) as T;
  }

  destroyAll(): void {
    for (const registry of this.registries.values()) {
      registry.destroy();
    }
  }
}

export class ChartRegistry {
  private chartMap = new Map<string, ChartScopedRegistries>();

  registerChart(chartId: string): void {
    if (!this.chartMap.has(chartId)) {
      this.chartMap.set(chartId, new ChartScopedRegistries(registryFactoryMap));
    }
  }

  getRegistry<T extends BaseRegistry<any>>(chartId: string, name: string): T | undefined {
    return this.chartMap.get(chartId)?.getRegistry(name);
  }

  deleteChart(chartId: string): void {
    const scoped = this.chartMap.get(chartId);
    if (scoped) {
      scoped.destroyAll();
      this.chartMap.delete(chartId);
    }
  }

  clearAll(): void {
    for (const [_, scoped] of this.chartMap.entries()) {
      scoped.destroyAll();
    }
    this.chartMap.clear();
  }
}
