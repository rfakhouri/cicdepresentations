# Cypress Hands On Test

0. Clone the following repo https://github.com/csps-efpc-daan-students-etudiants/intro-to-azure-devops-handson
    `git clone https://github.com/csps-efpc-daan-students-etudiants/intro-to-azure-devops-handson.git`
0. Bring up the database and api with `docker-compose up -d express-api` to run the web api and database in headless mode.
0. Navigate to `./vue-client` and run `npm run test:e2e` 
0. Write a test that enters a value in the text box, clicks the button, and then ensures that the text is added to the bottom of the list. 


