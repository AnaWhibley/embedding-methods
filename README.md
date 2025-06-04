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
