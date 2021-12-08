# Nestjs Monorepo 

##### Monorepo with nestjs
 - docker
 - secrets service
 - logs service
 - error handler
 - libs structure
 - dependency inversion pattern
 - anti corruption layer pattern
 - adapter pattern
 - swaggger documentation
 - tests
    - unit
    - e2e
---

#### Instalation

 - install monorepo dependencies
    ```bash
    $ yarn monorepo:install
    ```
 - install project dependencies 
    ```bash
    $ yarn workspace <workspaceName> install
    ```
 - install lib on project
    ```bash
    $ yarn workspace <workspaceName> add <libName>
    ```
##### workspace list
 - @app/eslint.config
 - @app/libs
 - @app/main.api
 - @app/other.api
---

#### Running the app
 - local
    ```bash
    $ yarn start:main
    $ yarn start:other
    ```

 - dev/hml/prd environment
    ```bash
    $ docker-compose up --build
    ```

#### Tests
 - unit
    ```bash
    # run monorepo tests
    $ yarn test
    ```
    
    ```bash
    # Run project tests
    $ yarn test main.api
    $ yarn test other.api
    $ yarn test libs
    ```
 - e2e
    ```
    $ yarn test:e2e
    ```
 - coverage
    ```
    $ yarn test:coverage
    ```

#### Lint

 - Run monorepo lint 
    ```bash
    $ yarn lint
    ```
 - Run project lint
    ```
    $ yarn workspace <workspaceName> lint
    ```

#### Build

 - Run project build
    ```
    $ yarn build <workspaceName>
    ```

#### Usage

 - logs
    ```js
    import { ILoggerService } from '@libs/modules';
    
    export class Exmeple {
      constructor(private readonly loggerService: ILoggerService) {}
    
      async exemple(): void {
        this.loggerService.log('message', 'messageContext');
        this.loggerService.error('error', 500, 'errorContext');
      }
    }
    ```
  - Secrets
    ```js
    import { ICommonSecrets } from '@libs/modules';
    
    export class Exmeple {
      constructor(private readonly secretService: ICommonSecrets) {}
    
      async exemple(): void {
        this.secretService.PORT;
      }
    }
    ```
 - Error exception

    ```js
    import { ApiException } from '@libs/utils';
    
    export class Exmeple {
      async exemple(): void {
        throw new ApiException('Error', HttpStatus.INTERNAL_SERVER_ERROR)
      }
    }
    ```
  - Http
      ```js 
      import { IHttpService } from '@libs/modules';
      export class Example {
         constructor(
            private readonly httpService: IHttpService,
         ) {}

         async exemple(): Promise<string> {
            const { data } = await this.httpService.http.get('http://url');

            return data.message;
         }
      }
      ```
### Adding new API

  - clone 
   ```base
   git clone https://github.com/mikemajesty/other-api.git
   ```

-- Example App Skeleton
```
.
├── apps
│   ├── main-api
│   │   ├── Dockerfile
│   │   ├── jest.config.js
│   │   ├── package.json
│   │   ├── src
│   │   │   ├── main.ts
│   │   │   └── modules
│   │   │       ├── health
│   │   │       │   ├── adapter.ts
│   │   │       │   ├── controller.ts
│   │   │       │   ├── module.ts
│   │   │       │   ├── service.ts
│   │   │       │   ├── swagger.ts
│   │   │       │   └── __tests__
│   │   │       │       ├── controller.e2e.spec.ts
│   │   │       │       ├── module.spec.ts
│   │   │       │       └── service.spec.ts
│   │   │       ├── module.ts
│   │   │       └── __tests__
│   │   │           └── module.spec.ts
│   │   ├── tsconfig.build.json
│   │   └── tsconfig.json
│   └── other-api
│       ├── Dockerfile
│       ├── jest.config.js
│       ├── package.json
│       ├── src
│       │   ├── main.ts
│       │   └── modules
│       │       ├── health
│       │       │   ├── adapter.ts
│       │       │   ├── controller.ts
│       │       │   ├── module.ts
│       │       │   ├── service.ts
│       │       │   ├── swagger.ts
│       │       │   └── __tests__
│       │       │       ├── controller.e2e.spec.ts
│       │       │       ├── module.spec.ts
│       │       │       └── service.spec.ts
│       │       ├── module.ts
│       │       └── __tests__
│       │           └── module.spec.ts
│       ├── tsconfig.build.json
│       └── tsconfig.json
├── CHANGELOG.md
├── commitlint.config.ts
├── devops
│   └── tag-create.sh
├── docker-compose.yml
├── jest.config.e2e.ts
├── jest.config.ts
├── libs
│   ├── core
│   │   └── index.ts
│   ├── jest.config.js
│   ├── modules
│   │   ├── http
│   │   │   ├── adapter.ts
│   │   │   ├── index.ts
│   │   │   ├── module.ts
│   │   │   ├── service.ts
│   │   │   └── __tests__
│   │   │       ├── module.spec.ts
│   │   │       └── service.spec.ts
│   │   ├── index.ts
│   │   ├── logger
│   │   │   ├── adapter.ts
│   │   │   ├── index.ts
│   │   │   ├── module.ts
│   │   │   ├── service.ts
│   │   │   └── __tests__
│   │   │       ├── module.spec.ts
│   │   │       └── service.spec.ts
│   │   ├── module.ts
│   │   ├── secrets
│   │   │   ├── adapter.ts
│   │   │   ├── enum.ts
│   │   │   ├── index.ts
│   │   │   ├── module.ts
│   │   │   ├── service.ts
│   │   │   └── __tests__
│   │   │       ├── module.spec.ts
│   │   │       └── service.spec.ts
│   │   └── __tests__
│   │       └── module.spec.ts
│   ├── package.json
│   ├── tsconfig.json
│   └── utils
│       ├── exception.ts
│       ├── filters
│       │   ├── http-exception.filter.ts
│       │   └── __tests__
│       │       └── http-exception.filter.spec.ts
│       ├── index.ts
│       ├── interceptors
│       │   ├── http-exception.interceptor.ts
│       │   └── __tests__
│       │       └── http-exception.interceptor.spec.ts
│       ├── static
│       │   └── htttp-status.json
│       ├── swagger.ts
│       └── __tests__
│           └── exception.spec.ts
├── nest-cli.json
├── package.json
├── README.md
├── tests
│   ├── common.js
│   ├── index.js
│   ├── main-api.js
│   └── other-api.js
├── tools
│   └── eslint
│       └── package.json
├── tsconfig.build.json
└── tsconfig.json
```

---
 #### Architecture
 - ```├── tools```: Project  tools like: eslint, prettier and etc.
 - ```├── libs```: Application shared libs.
 - ```├── libs ├── core```: Core business rules, don't use nestjs dependecies here, only class and rules that will be shared with other projects
 - ```├── libs ├── modules```: Application modules, use only nestjs modules here, you can add modules like: http, databse etc.
 - ```├── libs ├── utils```: Application utils, utilities that will shared with your monorepo.
 - ```├── apps```: Monorepo Applications.
 - ```├── tests```: Monorepo tests initializer like: env, mocks and configs.

---

The following is a list of all the people that have contributed to nest-boilerplate. Thanks for your contributions!

[<img alt="mikemajesty" src="https://avatars1.githubusercontent.com/u/11630212?s=460&v=4&s=117" width="117">](https://github.com/mikemajesty)

## License

It is available under the MIT license.
[License](https://opensource.org/licenses/mit-license.php)
