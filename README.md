# @nestjs-logger-config/nestjs-logger-config

[![npm version](https://badge.fury.io/js/%40nestjs-logger-config%2Fnestjs-logger-config.svg)](https://badge.fury.io/js/%40nestjs-logger-config%2Fnestjs-logger-config)
[![Downloads](https://img.shields.io/npm/dm/@nestjs-logger-config/nestjs-logger-config.svg)](https://npmjs.org/package/@nestjs-logger-config/nestjs-logger-config)
[![GitHub Issues](https://img.shields.io/github/issues-raw/yourusername/nestjs-logger-config.svg)](https://github.com/yourusername/nestjs-logger-config/issues)
[![GitHub license](https://img.shields.io/github/license/yourusername/nestjs-logger-config.svg)](https://github.com/yourusername/nestjs-logger-config/blob/master/LICENSE)

Zero-config logger setup for NestJS using JSON or TypeScript configuration files. Supports **Winston** & **Pino**.

## 🚀 Features

- ✅ **Zero code** - Configure via JSON/TypeScript file
- ✅ **Auto-detect** Winston or Pino from `package.json`
- ✅ **Strict validation** with Zod schemas
- ✅ **Environment variables** substitution `${VAR}`
- ✅ **Redaction** of sensitive data (passwords, tokens)
- ✅ **Multiple transports** (console, file, HTTP)
- ✅ **Request context** injection (requestId, userId)
- ✅ **TypeScript first** - Full type safety
- ✅ **Performance optimized** Pino support

## 📦 Installation

```bash
npm i @nestjs-logger-config/nestjs-logger-config
# Choose ONE logger:
npm i winston winston-daily-rotate-file  # OR
npm i pino pino-pretty pino-http
```

## ⚙️ Usage

1. Create config file (logger.config.json)

```json
{
  "provider": "winston",
  "service": "my-api",
  "level": "info",
  "format": "json",
  "redact": ["password", "token"],
  "transports": [
    { "type": "console" },
    { "type": "file", "filename": "logs/app.log" }
  ]
}
```

2. Setup in app.module.ts

```typescript
import { Module } from '@nestjs/common';
import { LoggerConfigModule } from '@nestjs-logger-config/nestjs-logger-config';

@Module({
  imports: [
    LoggerConfigModule.forRoot('./logger.config.json'),
  ],
})
export class AppModule {}
```

3. Use in main.ts

```typescript
import { NestFactory } from '@nestjs/core';
import { LoggerConfigService } from '@nestjs-logger-config/nestjs-logger-config';

async function bootstrap() {
  const app = await NestFactory.create(AppModule, { bufferLogs: true });
  const loggerService = app.get(LoggerConfigService);
  app.useLogger(loggerService.getLogger());
  await app.listen(3000);
}
bootstrap();
```

## 🎯 Examples
See examples folder for complete working examples.

## 📚 Documentation
Full documentation coming soon!

## 🤝 Contributing
Contributions welcome! See CONTRIBUTING.md.

## 📄 License
MIT License - see LICENSE