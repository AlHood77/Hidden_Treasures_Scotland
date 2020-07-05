HIDDEN TREASURES SCOTLAND

The app to discover mini adventures near you.
You can search our growing API to find unusual places to visit in and around Scotland. Hidden beaches, caves, walks and generally fun places for a mini adventure in your back yard.

## MVP
User can find places close to them based on their location, using the leaflet library map for Vue.js.
Places have latitude and longitude, name, description, images & comments.
Data is accessible via a JSON API, stored in MongoDB.
Users can submit new places to the API.

**Vue Components**
- Map
- Place Select and Filter
- Add new Place
- Place Comments
- Place Information

## Running the site locally

1. In MongoDB create a database called treasures

2. Once you've pulled the code down from github go into the "client" and "server" folders and run npm i in both folders

3. In the server folder seed the database npm run seeds

4. Run the Express server, npm run server:dev and visit this url to make sure the data from the seeds file is there, http://localhost:3000/api/facts/

5. Now you can now either run the client locally going into the client folder running npm run serve then go most likely to http://localhost:8080/ in your browser
