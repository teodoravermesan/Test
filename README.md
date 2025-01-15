1. create a folder and open it in vscode
2. init cypress
npm init
npm install cypress --save-dev
npx cypress open
3. config cypress and add new spec: cypress\e2e\test.cy.js
4. create HTML Reports
- npm install --save-dev mochawesome mochawesome-merge mochawesome-report-generator
- cypress run --reporter mochawesome
- config cypress.config.js
const { defineConfig } = require("cypress");

module.exports = defineConfig({
  reporter: "mochawesome",
  reporterOptions: {
    reportDir: "cypress/results",
    overwrite: false,
    html: true,
    json: true,
  },
  e2e: {
    setupNodeEvents(on, config) {
      // implement node event listeners here
    },
  },
});

- npx cypress run --reporter mochawesome   --reporter-options reportDir="cypress/results",overwrite=false,html=false,json=true
6. push code to git
- git init
- git add .
- git commit -m "test"
- publish branch: 
- git push origin master
7. integrate with jenkins
- New item > freestyle project
- Source Code Management: git: https://github.com/teodoravermesan/test
- Build steps: Execute Windows batch command
npm i
npx cypress run
- Post-build Actions: Publish HTML reports
HTML directory to archive: C:\Users\tvermesan\OneDrive - RWS\Desktop\test\cypress\results
Index page[s]: mochawesome.html
Report title: Report

Note: if html report is blank:

- System.setProperty("hudson.model.DirectoryBrowserSupport.CSP","")

