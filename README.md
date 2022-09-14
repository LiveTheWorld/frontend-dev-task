# frontend-dev-task

This task is designed towards delivering a detail landing page for our activities. We have intentionally provided just the basic guidelines and a wireframe. 

Considering the nature of the role you'll be required to give your own inputs and collaborate with the team on the UX, so figuring out the UX for this task is upto you.

### You can use either `React.js or Vue.js` for this task's implementation. 

Remember you can contact me at ali@livetheworld.com incase you've any questions. You will not be penalized at all for asking questions.


## Description

You'll be implementing a ACTIVITY'S DETAIL PAGE, similar to our current detail page e.g. here https://www.livetheworld.com/activities/belgium/castle-of-gerald-the-devil but obviously with not all the details and functionalities 😁 

`We do suggest you to visit our activity's pages and explore around for a few minutes so that you get the gist of what you are supposed to implement and get inspiration from there.`

You can find the wireframe for this page here along with the added sticky notes for guidance where necessary: https://lucid.app/lucidchart/3a830004-3d26-499c-83d5-a11c916f752a/edit?invitationId=inv_fc0bd1b0-b224-402f-a456-56e10e2f4ada&page=0_0#  `You can quickly create an account for free here using your email to view the wireframe`

Page should be viewable only by a signed in user `You should have received your test user credentials in the email`

To access the endpoints you'll be using the following base url: `https://ltw-cms-stg.herokuapp.com` so e.g. the url of activity detail endpoint would become `https://ltw-cms-stg.herokuapp.com/frontend/activities/slug/:activity_slug`

## Must have features
- The page doesn't need to be detailed as the live one. Please go through the wireframe for the elements required in the page.

- URL of activity page should be `/:activity_slug`. Following are some of the existing activity's slugs which you can use to test your development: castle-of-gerald-the-devil , belfry-of-ghent , birth-forest-geboortebos

- You'll fetch the activity's detail using following api
    ```
      ENDPOINT:  /frontend/activities/slug/:activity_slug
      REQUEST TYPE: GET
      ^ This endpoint returns you the details of the activity. Below mentioned are the response fields you'll need. See the wireframe https://lucid.app/lucidchart/3a830004-3d26-499c-83d5-a11c916f752a/edit?invitationId=inv_fc0bd1b0-b224-402f-a456-56e10e2f4ada&page=0_0# to get an understanding of what you'll use where

      RESPONSE: 
      {
        ...,
        id,
        slug,
        description_short,
        description_long, // IT WILL BE A MARKDOWN HTML STRING SO USE ACCORDINGLY ON FRONTEND, TO GET AN IDEA I'LL SUGGEST YOU TO VIEW SOME OF OUR EXISTING ACTIVITIES
        latitude,
        longitude,
        images,
        labels
      }
  ```
- Page should be viewable only by a signed in user `You should have received your test user credentials in the email`
- Incase a non signed-in user lands on the page, show a popup / modal for login on top of the activity page. It should just take the email and password and do the login hit. Here are the details of login api.
  ```
      ENDPOINT:  /auth/local/
      REQUEST TYPE: POST
      REQUEST BODY: {identifier, password}
      ^ This endpoint expects email of user in the identifier field and the password.

      RESPONSE: 
      {
        "jwt": "token", // USE THIS TOKEN FOR REQUESTING USER TRIPS MENTIONED IN POINTS BELOW
        "user": { first_name, last_name, ...  }
      }
  ```
- Once the user logins,,, popup should disappear and the activity's details beneath should be visible.
- For logged in user, do the user trips api hit to fetch the user's existing trips, based on the response you'll be able to show whether the user already has saved particular activity or not.

  ```  
      ENDPOINT:  /frontend/trips
      REQUEST TYPE: GET
      ^ While calling this endpoint you should be sending the authentication jwt token in headers too which you received earlier in login response.
      e.g. Authorization: `Bearer your_token`

      Based on this api response show current status save/saved of the current activity. Also for all the nearby activities ( mentioned in points below )
      
      SAMPLE RESPONSE: 
      [
         ... ,
         {
            id: int // ID OF YOUR FAVORITE TRIP
            type: "favorite",
            activities : [ARRAY] // go through this array of activities to see which activities user has already added to favorites
         }
      ]
  ```
- If the current activity is already added to favorites show SAVED else SAVE in the SAVE BUTTON mentioned on wireframe.
- You'll also be needed to show a carousel for nearby activities ( see wireframe ). To fetch the nearby activities in vicinity of the current one, use the current activity's id which you received earlier in activity's endpoint
   ```  
      ENDPOINT:  /frontend/activities/nearby/:activity_id
      REQUEST TYPE: GET

      Based on this api response show all nearby activity's and also their save status as per wireframe. ( Whether any activity is added to favorites or not you already have the data in trips api above
      
      SAMPLE RESPONSE: 
      [
         ... ,
         {
            id: int,
            slug: string,
            images : [ARRAY],
            description_short: string
         }
      ]
  ```
 - A signed in user should also be able to add the current activity or any activity nearby activities to his favorites. You'll have to use following endpoint for this:
  ```  
      ENDPOINT:  /frontend/trips/add_activity
      REQUEST TYPE: PUT
      REQUEST BODY: 
      {
        activityId: // ID OF ACTIVITY TO ADD
        tripId: // ID OF YOUR FAVORITE TRIP WHICH YOU RECEIVED IN TRIPS API
        tripType: "favorite"
      }
      ^ While calling this endpoint you should be sending the authentication jwt token in headers too which you received earlier in login response.
      e.g. Authorization: `Bearer your_token`

      In case of success update acitivities' save status on page accordingly.
  ```
 - A signed in user should also be able to remove the current activity or any activity nearby activities from the favorites. You'll have to use following endpoint for this:
  ```  
      ENDPOINT:  /frontend/trips/remove_activity
      REQUEST TYPE: PUT
      REQUEST BODY: 
      {
        activityId: // ID OF ACTIVITY TO ADD
        tripId: // ID OF YOUR FAVORITE TRIP WHICH YOU RECEIVED IN TRIPS API
        tripType: "favorite"
      }
      ^ While calling this endpoint you should be sending the authentication jwt token in headers too which you received earlier in login response.
      e.g. Authorization: `Bearer your_token`

      In case of success update acitivities' save status on page accordingly.
  ```

## Nice to have features
- All the activity images whether in the top carousel or the nearby carousel should be lazy loaded.
- Suppose a user has opened multiple tabs at the same time. Incase the user adds/remove an activity from `FAVORITES` the `SAVE STATUS` of activities should remain updated across the tabs of same browser. You'll have to figure out how. 😊


## Implementation Guidelines


Must haves:
- You should use either React.js or Vue.js for this task
- We rely heavily on state management for our frontend apps, so please do use state management for your task too.
- Deploy the project and make it available in some public URL ( you can use heroku, netlify, aws etc whichever you are comfortable with )
- A clear README on how to locally set up your submission repo.
- README file of your repo should also clearly mention any assumptions you made or any nice to have features you added.
- A clear history of your commits on the github repo for the project.

NOTES:
- Use any UI framework of your comfort
- There are no marks for a heavily designed UX but it still needs to be plain, simple and mobile responsive ofcourse :)

## Evaluation
In this assignment we would like you to showcase the following skills:
- Proficiency with Javascript and React/Vue
- Developing clean, well-documented and easily testable code in line with best practices
- Handling errors properly
- Developing working, bug-free features
- Ability to understand and interpret functional requirements
- Ability to understand and use APIs
- Ability to use git and Github and its best practices

You should be able to complete this task within 6-8hrs.
Let us know what still has be to done, in case you didn't manage to complete everything.

`Also in your submission please do mention the time you spent on the task.`


## Submission
- You should upload your code to Github repositories (public) and share it with us. 
- Also please share the live url to the deployed app.
- Your repositories should have a README.md that explains how to run the code and any other notes that are important.

### Looking forward to see your submission. HAPPY CODING 🎉
