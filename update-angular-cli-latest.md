
## update angular/cli

```bash
npm uninstall -g angular-cli
npm cache clean or npm cache verify (if npm > 5)
npm install -g @angular/cli@latest
```

## update core
```bash
ng update @angular/core
```

## update rxjs

```bash
ng update rxjs
```

After updating both the global and local package, clear the cache to avoid errors:

## After updating both the global and local package, clear the cache to avoid errors

```bash
npm cache verify (recommended)
npm cache clean (for older npm versions)
```
