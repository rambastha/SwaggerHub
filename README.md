# SwaggerHub
MyProject
name: API Standardization
​
# Controls when the action will run. 
on:
  # Triggers the workflow on pull request events but only for the main branch
  pull_request:
    branches: [ main ]
​
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:
​
# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  build:
    runs-on: ubuntu-latest
​
    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2
​
      - name: Use Nodejs 12.x
        uses: actions/setup-node@v1
        with:
          node-version: "12.x"
      - run: npm install swaggerhub-cli -g && npm install js-yaml
          
      - name: API Standardization
        if: ${{ success() }}
        run: |
          swaggerhub api:validate [api location in swaggerhub]
          swaggerhub api:publish [api location in swaggerhub]
          swaggerhub api:setdefault [api location in swaggerhub]
        env:
          SWAGGERHUB_API_KEY: [enter api key]
