## Frontend Deployment Steps for Logistix 📌 for [dev](https://logistix.dev/) and [uat](https://uat.logistix.dev/)


---


- Update the nuxt.config.ts file with following fields (only for uat)
```
1. `typeCheck: false`
2. `ssr: false`
```

- Remove .output from .gitignore file

- Redirect to _main_ branch and get latest code
```
git checkout main

```
```
git pull

```

- Switch to the _uat_ branch / _dev_ branch
- 
```
git checkout uat

```

- Merge _main_ into specified branch

```
git pull origin main

```

- Install yarn dependencies

```
yarn

```

- Generate Yarn.

```
yarn generate

```


- Push changes to specified branch after successful yarn generation

```
git add .
git commit -m "commit-message"
git push

```

## Digital Ocean server Setup

- Go to Digital Ocean, click on the respective droplet and click _console_

```
cd code/logistix-web

```

- Take the latest pull

```
git pull

```

- Provide Git username and password 

- copying the contents of the directory to the specified directory

```
cp -r .output/public/ /var/www/new

```
- Change directory to /var/www/

```
cd /var/www/

```
- Remove prev file

```
  rm -rf prev

```
  - Move html to prev

```
  mv html prev

```
  - Move new to html

```
  mv new html

```

!!NOTE : 
These revisions aim to improve clarity and ensure consistency in the steps provided. Make sure to adapt them according to your project's specific needs.
