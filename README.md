# React_Github_Actions-Sample

## Github actions parallel jobs (test and deploy)
In the following case we set two jobs (test and deploy):

The first job (test) runs on a Linux virtual machine (agent) where is installed the "ubuntu-latest" operating system
- Get the code with the "action/checkout@v3"
- Install NodeJS with the "actions/setup-node@v3"
- Install the app dependencies with the "npm ci" command
- Run tests with the "npm test" command

The second job (deploy) also runs on a Linux virtual machine (agent) where is installed the "ubuntu-latest" operating system
- Get the code with the "action/checkout@v3"
- Install NodeJS with the "actions/setup-node@v3"
- Install the app dependencies with the "npm ci" command
- Build the project with the "npm run build" command

See the build.yml file source code for executing two parallel jobs (test and deploy):
  
```yml
name: Test Project
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install NodeJS
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Get code
        uses: actions/checkout@v3
      - name: Install NodeJS
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci
      - name: Build project
        run: npm run build
      - name: Deploy
        run: echo "Deploying ..."
```


## Github actions secuential jobs (test and deploy)
For example if we require to finish the test before starting the deploy jon then use the "needs" tag. See the example:

```yml
deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Get code
```

This is the final code:

```yml


```
