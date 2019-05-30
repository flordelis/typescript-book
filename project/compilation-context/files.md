# Which Files?

You can either use `files` to be explicit:

```javascript
{
    "files":[
        "./some/file.ts"
    ]
}
```

or `include` and `exclude` to specify files / folders / globs. E.g.:

```javascript
{
    "include":[
        "./folder"
    ],
    "exclude":[
        "./folder/**/*.spec.ts",
        "./folder/someSubFolder"
    ]
}
```

Some notes:

* For globs : `**/*` \(e.g. sample usage `somefolder/**/*`\) means all folder and any files \(the extensions `.ts`/`.tsx` will be assumed and if `allowJs:true` so will `.js`/`.jsx`\)

