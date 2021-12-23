# LearningNestJS

### Introduction 

- NestJS ia a framework for building efficient, scalable Node.js server-side applications. It uses progressive JavaScript, is built with and fully supports TypeScript, and combines elements of OOP (Object Oriented Programming), FP (Functional Programming), and FRP (Functional Reactive Programming).

- Underneath, Nest makes use of robust HTTP Server frameworks, like Express.

- NestJS was created to solve the main problem of a server-side JavaScript application, the Architecure.

### Installation

- `npm i -g @nestjs/cli`
- `nest new hello-world`
- `cd hello-world`
- `npm run start`

### First steps

- We will build a basic CRUD application with features that cover a lot of ground at an introductory level.
- After installation, the `hello-world` directory will be created, node modules and a few other boilerplate files will be installed, and a `src/` directory will be created and populated with several core files.

src  
 |  
 |- app.controller.spec.ts: The unit tests for the controller  
 |- app.controller.ts: A basic controller with a single route  
 |- app.module.ts: The root module of the application  
 |- app.service.ts: A basic service with a single method  
 |_ main.ts: The entry file of the application which uses the core function `NestFactory` to create a Nest application instance  
 
- The `main.ts` includes an async function, which will **bootstrap** our application. In the example below, we simply start up our HTTP listener, which lets the application await inbound HTTP requests.

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

#### Running the aplication

- Once the installation process is complete, you can run the command `npm run start`. Now the application is able to listen for inbound HTTP requests.

### Controllers

- In order to create a basic controller, we use classes and **decorator**. Decorators associate classes with required metadata and enable Nest to create a routing map (tie requests to the corresponding controllers).

### Routing

- In the following example we´ll use the `@Controller` decorator, which is required to define a basic controller. We´ll specify an optional route path prefix of `cats`. Using a pth prefix in a `@Controller` decorator allows us to easily group a set of related routes, and minimize repetitive code.
- @Get is the HTTP request method.
- The current path for the returning of all cats is `GET /cats`
- If we had added a @Get decorator @Get('small'), the path would be `GET /customers/profile`
- The findAll method here is completely arbitrary, Nest doesn´t attach any significance to the method name chosen
- The response´s **status code** is always 200 by default, except for POST requests which use 201. For change this behavior, just add @HttpCode(...) after @Get.

```
import { Controller, Get } from "@nestjs/common";

@Controller('cats')
export class CatsController {
  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}
```

### Resources

- For create a **POST** handler, it´s quite simple, see the code below:

```
import { Controller, Get, Post } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Post()
  create(): string {
    return 'This action adds a new cat';
  }

  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}
```

- Nest provides decorators for all standard HTTP methods: `@Get()`, `@Post()`, `@Put()`, `@Delete`, `@Patch()`, `@Options()` and `@Head`. In addition, `@All()` defines an endpoint that handles all of them.

### Status code

- By default 200 is always the status code. We can change this behavior by adding the `@HttpCode(...)` decorator at a handler level

```
import { Controller, Get, Post, HttpCode } from "@nestjs/common";

@Controller('cats')
export class CatsController {
  @Post()
  @HttpCode(204)
  create(): string {
    return 'This action adds a new cat';
  }

  @Get() // @Get is the HTTP request method
  findAll(): string { // The findAll method here is completely arbitrary, Nest doesn´t attach any significance to the method name chosen
    return 'This action returns all cats';
  }
}
```

### Headers

- To specify a custom header, we can use a `@Header()` decorator, as follows:

```
  import { Controller, Get, Post, HttpCode, Header } from "@nestjs/common";
  
  ...
  
  @Post()
  @Header('Cache-Control', 'none')
  create() {
    return 'This action adds a new cat';
  }
```

### Route parameters 

- To use params, see below:

```
@Get(':id')
findOne(@Param() params): string {
  console.log(params.id);
  return `This action returns a #${params.id} cat`;
}
```

### Asynchronicity

- Nest supports and works well with `async` functions.





 
 
 
