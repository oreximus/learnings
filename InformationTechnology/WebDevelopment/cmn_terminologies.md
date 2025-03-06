## Common Terminologies and their definitions in website development:

- `global pipes`: Global pipes in NestJS are a powerful feature that allows you to apply data transformation and validation
  across your entire application automatically. They are set up to process incoming data for all route handlers without the
  need to explicitly bind them to each controller or method.

- To setup up a global pipe in NestJS, you typically add it in the main.ts file of your application:

```
import {ValidatePipe} from "@nestjs/common";
import {NestFactory} from "@nest/core";
import {AppModule} from "./app.module";

async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    app.useGlobalPipes(new ValidatePipe());
    await app.listen(3000);
}

bootstrap();
```

- This setup applies the ValidationPipe globally, which means it will automatically validate incoming request data based
  on your DTO (Data Transfer Object) classes.

> `Data Transfer Object`: A Data Transfer Object (DTO) is an object used to encapsulate and transfer data between different
> parts of a software application. DTOs serve serveral important purposes:

    1. **Data Encapsulation**: DTOs package related data fileds into a single object, simplifying data transfer between
    application layers or subsystems.
    2. **Network Efficiency**: In distributed systems, DTOs reduce the number of network calls by aggregating data that
    would otherwise require multiple separate requests.
    3. **Separation of Concerns**: DTOs help decouple different layers of an application, particularly between the service
    layer and the user interface.
    4. **Data Simplification**: They provide a simplified view of complex internal data structures, exposing only
    necessary information to other parts of the system.
    5. **Security Enhancement**: DTOs can be used to control which data is exposed, helping to protect sensitive
    information.

- Key benefit of using global pipes includes:

  1. Consistent data validation across all endpoints
  2. Automatic transformation of incoming data to the correct types
  3. Reduced boilerplace code, as you don't need to apply pipes to individual routes
  4. Centralized error handling for invalid data

- Global pipes are particularly useful for tasks like data validation, where you want to ensure all incoming requests meet
  certain criteria before they reach your route handlers.
