import java.util.HashMap;
import java.util.Map;

public class AnotherDIExample {

    public static void main(String[] args) {
        // Create a DI container
        DIContainer diContainer = new DIContainer();

        // Register dependencies
        diContainer.registerDependency(ServiceInterface.class, new AnotherServiceImplementation());

        // Resolve dependencies
        ServiceInterface service = diContainer.resolveDependency(ServiceInterface.class);

        // Use the service
        service.doSomething();
    }

    // Interface for services
    interface ServiceInterface {
        void doSomething();
    }

    // Another implementation of ServiceInterface
    static class AnotherServiceImplementation implements ServiceInterface {
        @Override
        public void doSomething() {
            System.out.println("Another service is doing something.");
        }
    }

    // Simple DI container
    static class DIContainer {
        private Map<Class<?>, Object> dependencies = new HashMap<>();

        // Register dependency
        public <T> void registerDependency(Class<T> type, T instance) {
            dependencies.put(type, instance);
        }

        // Resolve dependency
        public <T> T resolveDependency(Class<T> type) {
            return type.cast(dependencies.get(type));
        }
    }
}
