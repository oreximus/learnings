## Nest JS Tutorial

**source**: https://www.youtube.com/watch?v=8_X0nSrzrCw&t=94s

### Why NestJS so popular?

- It's opinionated, well-structured architecture, TypeScript support, scalability, and
  a strong community.

- Under the hood, Nest makes use of robust HTTP Server frameworks like **Express** (the
  default) and optionally can be configured to use **Fastify** as well.

- Nest (NestJS) is a framework for building efficient, scalable **Node.js** server-side
  applications. It uses progressive JavaScript, is built with and fully supports
  **TypeScript** (yet still enables developers to code in pure JavaScript) and combines
  elements of OOP (Object Oriented Programming), FP (Functional Programming), and FRP
  (Functional Reactive Programming).

### Getting Started with NestJS Project:

- installing nestjs cli utility globally:

```
npm i -g @nestjs/cli
```

- creating a nestjs project:

```
nest new <project_name>
```

- select your package manager and you're good to go!

### Notes from the nestjs official docs:

**source**: https://docs.nestjs.com/first-steps

- By default, if any error happens while creating the application our app will
  exit with the code `1`. If we want to make it throw an error instead disable
  the option `abortOnError` (e.g. `NestFactory.create(AppModule, {abortOnError: false})`).

- To quickly create a CRUD controller with built-in `validation`, you can use the CLI's
  CRUD generator: `nest g resource [name]`.

#### NestFactory:

**source**: perplexity.ai

- `NestFactory`: NestFactory is a core class in NestJS that provides static
  methods for creating application instances. it is used to bootstrap and
  initialize a NestJS application, serving as the entry point for creating
  different types of applications such as web servers, microservices, and
  standalone applications.

- The `NestFactory` class offers several key methods:

  1. `create()`: This method creates an instance of NestApplication, which
     is typically used for creating HTTP-based server-side applications.
  2. `createMicroservices()`: This method is used to create an instance
     of NestMicroservice, specifically designed for building microservices.
  3. `createApplicationContext()`: This method creates an instance of
     NestApplicationContext, which is useful for creating standalone
     applications or when you need a Nest container without a network layer.

- These methods allow developers to configure the application instance,
  set up middleware, and define the root module of the application. The
  NestFactory provides a flexible way to bootstrap different types of
  NestJS application, making it a crucial component in the framework
  architecture.

#### Routing

- In the following example, we'll use the `@Controller()` decorator, which is **required**
  to define a basic controller. We'll specify an optional route path prefix of `cats`.
  Using a path prefix in the `@Controller()` decorator help us group related routes
  together and reduces repetitive code.

- For example, if we want to group routes that manage interaction with a cat entity
  under the `/cats` path, we can specify the `/cats` path prefix in the `@Controller()`
  decorator. This way, we don't need to repeat that portion of the path for each route in
  the file.
