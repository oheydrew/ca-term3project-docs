<img src="assets/images/chicken-in-logo.png">

## 'CHICKEN IN' - RED ROCKS CHARCOAL CHICKEN
### TIMESHEET AND OVERTIME TRACKING SYSTEM

Coder Academy Group Project 2017 by Drew, Maxi, Shun and Winter - **Team Painframe**

<br>

----
<br>

# 1. Who is your client?
Our client, Edwin Huang, owns and operates a number of charcoal chicken shops around Victoria, under the brand name “Red Rocks Charcoal Chicken”. He splits his time between working in the stores as a manager, and doing all the administrative/entrepreneurial work as the owner.

Red Rocks Charcoal Chicken is a small group of chicken shops all owned by the same owner. They aren't a franchise, more a small group owned by the same group. A lot of their regular employees are students, and as they aren't a very technologically invested company, they are still doing their time-sheets and overtime calculations manually. 

Red Rocks Charcoal Chicken have little to no branding (Besides the colours Red and White and various "chicken" mascot logos) to speak of, and almost no internet presence, so we did not have to worry about linking into an existing system. This was a challenge but also provided us with an opportunity to work on branding and style.

<br>
<br>

# 2. What is your client’s need (i.e. challenge) that you will be addressing in your project?
One of Edwin’s biggest challenges is keeping track of employee hours worked, calculating overtime and calculating how much he owes in wages to each employee. Currently, his employees record how many hours they’ve worked on a paper form, and he manually updates his excel spreadsheet at the end of the week. It’s time consuming work and his employees often make mistakes which means he has to manually follow up with those employees to clarify the situation.

We saw a lot of potential for being able to help him with his business needs- He suggested we could develop him a front-facing website that his clients could use to look up their locations and menus, but we felt that it wouldn't suit the scope of our project. In the end due to time and scope constraints, we decided with Edwin to work on a small app to take track of weekly hours worked by his staff, and calculate the number of overtime hours. 

Big considerations in this project are the differences in the ways in which different users will use the product. **Employees** will likely wish for a simple, quick, easy interaction with the software, *most likely on their mobile phones*. **Managers**, however, will want a lot more control, data display and interactivity with their end of the process. 

In both cases, the aim of this project will be to *help both the employees, and the managers, spend less time on the administrative chores of timesheets*. The mobile app for Employees, will need to be simple, responsive, and easy to use- and the app for the managers will need to do a lot of automatic calculation, organization and filtering, to make the managers' jobs easier and simpler. This is about giving them something they will *want* to use, not something that scares them away from the technology.  

We had the thought of making this app a "blank canvas" for inputting any other business's data in, and using it themselves, thus moving away from the specific Red Rock Charcoal Chicken instance, and into more of a reusable, resellable app - but decided to double-down and focus on the specific client that we have, and customize it to their needs (though, coding will be structured in a way that this could still be achievable).

As far as branding and naming, we had the idea of calling the app "Chicken-In" as a reference to "Checking In" to your shift. Edwin found this very funny, and agreed, as it is an internal, employee-facing app.

<br>
<br>

# 3. Describe the client’s current setup and data.
Red Rocks Charcoal Chicken does not currently implement a digital solution to this problem. They are currently using an excel spreadsheet to manage employee data and employee expenses. The managers of each store must manually update the spreadsheet at the end of every week- This is time consuming and could better be handled through the use of an app and database solution.

Ideally, it would be nice to be able to work with the client's current paper data system, but this would require scanning in documents and we believe this process would only serve to frustrate, not help the situation. Getting everybody on board with an app-based system and doing away with paper would be the most efficient solution.

<br>
<br>

# 4. Describe the project will you be conducting and how your App will address the client’s needs.
In keeping with the previous comments about doing away with paper, we will develop an online app that will enable Edwin’s employees to easily enter in the amount of hours they’ve worked, and allow the managers to log in, and administrate the process. The app will essentially have two parts: **Employee** and **Manager**

### - Employee Section
In the **Employee** section, the app will allow employees to log in, enter their shifts, and the app will automatically calculate the standard and overtime hours based on the information, and send this information back to our mongodb database for later retrieval by the **Manager** side of the app. The Employee will also be able to see the status of their entered shifts, from *pending*, to *approved* and *rejected*. 

This will have 2 main views (pages):
- Add Shift
- Employee Settings (Update password, etc)

### - Manager Section
In the **Manager** section, Ed or his managers, can add/remove employees from the system and review the submissions before *approving* them. The dashboard will also include an overview of past wages paid, which he filters by various fields (dates, locations, employee, etc).

This will have 4 main views (pages):
- Review/Approval
- Reporting / Filtering past shifts
- Add / Change / Remove Employees
- Business Settings (ie overtime rates, store locations etc)

If we have time, we would like to implement Data Visualization, as well.

This app will streamline the process of calculating wages, reduce the number of errors and remove the need to manually update an excel spreadsheet.

<br>
<br>

# 5. Identify and describe the software (including databases) to be used in your App.

### Frontend:
We will develop the frontend in JavaScript, using the React library. We will also use react-router to enable client-side routing and Webpack as our asset bundler. We intend to use custom styling with SCSS for the most part, subsidized by some premade components (such as the AirBNB DatePicker, and TimePicker components, which we will style accordingly).

We plan to do a lot of the calculations of hours and overtime here, in the front-end, to take advantage of client CPU resources and not overload our server.

For testing, we plan to implement Jest, and Enzyme for testing React components.

### Backend:
We will develop the backend in NodeJS, using the Express library to speed up the process. We will use custom middlewares for certain tasks, and plan to use PassportJS for Authentication, and PermitJS for Authorization.

The backend will mostly be handling security with cookies, Authentication and Authorization, as well as storage and removal of data in the database. It will also act as a main entry point for our whole app, serving the relevant front-end index.js entry points according to the client's authorization.

For testing, we plan to implement Jest for both Unit and Integration Tests. For Route Testing, we will use Supertest - a package that can make requests on behalf of our testing suite.

### Database: 
We will use MongoDB for our database. The plan is to install our database on the production server, as opposed to using a third-party database manager like Atlas or mLab, as this will give our app more speed. We'll use the mongoose library to interact with our database in our NodeJS Express backend. We will use Compass as a tool to inspect this database when necessary.

### Host:
We will use DigitalOcean to host our App. This is a cloud provider much like AWS or GCS, but with a much simpler, more hands-on approach. This will allow us to SSH in to a Linux Compute Server, and allow us to install Node, and run our server in a server process, and our MongoDB in another. 

To begin with, we plan to employ the initial production 'semi manually', by remote-accessing the server with SSH. If time permits, we plan to implement containerization using Docker, and a CI tool such as TravisCI to help automate the production process. We are sceptical that we will have time for this, however. 

<br>
<br>

# 6. Identify and describe the network setup you will use in your development.

Our app will not need to rely on any external network infrastructure. The system will be 'cloud based', that is, accessible through the internet for both employees and managers. This works best, especially for the employees, who will be able to access it from anywhere at any time.

Our app will live in a DiginalOcean virtual computer. Users will enter the domain name, chicken-in.com, into their browser and the server will handle their requests, serve them static assets and serve them data in JSON format. Users will interact with our app entirely on their phones, or web browser.

This will necessitate an understanding of Web and Internet infrastructure, as well as Internet Protocols and Production Environments. Our chosen production environment, digitalocean, will provide us with some new learnings along the way, but we are excited to tackle them.

<br>
<br>

# 7. Identify and describe the infrastructure (i.e. hardware) that your App will run on.

We will host our App on Digital Ocean. We will buy the cheapest plan, which gives us access to a virtual computer with 1GB of memory, 1vCPU, 25GB of SSD storage, and allow up to 1TB of transfers per month. We are planning to install our database on the server, so will not need to use third-party services like Atlas or mLab.

<br>
<br>

# 8. Describe the architecture of your App.

<a href="assets/images/architecture.jpg" target="_blank"><img src="assets/images/architecture.jpg" width="800"></a>

(Initial ideation / decision making process for our 3-app system, and other ideas)

## Overview:

```

/
-- /backend/
       /models/
           /Employee.js
           /Manager.js
           /Shifts.js
           /Business.js
       /routes/                              ## routes start here for each 
           /authRouter.js                    ## /api/route/ namespace
           /employeeRouter.js   
           /...etc                                      
       /controllers/                         ## ...and refer to 'controllers' 
           /employeeRouter.js                ## for their methods/logic
           /...etc                                  
       /middleware/
           /authMiddleware.js
           /logger.js
           /...etc
       /tests/
           /unit/
              /example.test.js
           /integration/
              /example.test.js
           /route/
              /example.test.js
       server.js                             ## Server Entry Point

-- /frontend/
      /dist/                                 ## webpack bundled production files
      /src/
          /employeeApp/
              /dashboardPage/
                  /exampleComponent/
                      exampleComponent.js
                      exampleComponent.scss
              /router/                       ## Shared Components live in router
                  /exampleComponent/
                      exampleComponent.js
                      exampleComponent.scss
                  /AppRouter.js              ## Main React Entry Point
              /settingsPage/
                  ## components go here
              /index.html                    ## Entry Point served by backend              
              /index.js
              /styles.scss                   ## Overall Page styles
          /managerApp/
              ## Same structure as above
          /guestApp/
              ## Same structure as above
          /img/
          /tests/

-- /node_modules/
-- /package.json
-- /README.md
-- /webpack.config.js
-- (other files ie .gitignore, .eslint.rc etc etc)
```

The otherarching Architecture of our App is that it will be one NodeJS Express App Backend, which serves 3 smaller React 'apps' in separate index.js entry points.

All of these higher level components will live in the same root folder structure under their own subfolders- with the package.lock and node_modules in the root- able to run the entire app with `npm run start` (and other dev commands).

This single-backend containing multiple-frontends approach allows for the entire app to be easily containerized and to have all our apps run from the same root using `npm run` commands. Each frontend app will be able to be dev served using `npm run dev-app` for development purposes.

## Frontend:

We will create three seperate frontend apps. 
- 'Guest' (a login portal, essentially)
- 'Employee'
- 'Manager' 

Once authenticated, within each frontend app we will utilise react-router to enable client-side routing within each app. These frontend apps will comminucate with our backend server via api requests.

Each app splits out into per-page (view) folders, with components (and style for each component) living in their own folders inside these. The first component, `router`, holds the `AppRouter.js`, which is the main React entry point, with the `React-Router` layout. From here, components are pulled in.

State will be managed within each page separately, inside the components which require them. Instead of using a large, complex "Redux" service, or an even more complex "Single Source" of state in the AppRouter, we opted to hold state in each page. This could get messy if the app were to scale, but in the scope and timeframe of the project we decided this simpler, stateful component style would serve us better, for now.

## Backend:

The backend app will be running a NodeJS Express server, running 'server.js' on our DigitalOcean virtual computer. Our server will listen for requests and handle them according to the endpoints that the requests go to. Our server will serve all the static files to the user, depending on the authorization details they provide.

#### Authorization and Authentication logic

The backend webserver will be set up to listen for requests at the '*' root, and direct them to the `Guest` app if they have no cookie, or an invalid cookie. They can select whether to login as an *Employee* or *Manager*, here (registration will be handled by Managers), and will forward them a cookie, then redirect them back to the root.

Upon arriving here a second time, the user will be logged in with the relevant cookie. This cookie will hold their authentication details, and whether they are authenticated for the *manager* or *employee* app. Our server will serve one of these these apps to the user, depending on the authorization details they provide. 

#### Routing and "Controller" logic

In most cases, route flow will be: 

`server.js` -> `/routes/exampleRouter.js` -> `/controllers/exampleController.js` -> `models/Example.js`

Routing will be handled by routes files, scoped to each API Endpoint. From here, these routes are pulled in, and each "GET", "POST", etc is routed through to `controllers`, which are also namespaced to their endpoint. The logic in breaking these routes out into routes and controller is around keeping the `routes` files cleaner and more readable, giving us an easy way to see the routes that have been created, and keep it neat and tidy.

Controllers will be where any logic and calculations are needed to be done. Authorization and Authentication logic will be held in their own controller, and be a lot more complex than the simple "CRUD" logic needed by most the other endpoints. 

The models themselves will be required into the controllers, so they can used them.

## Database:

We are planning to install a MongoDB database on our DigitalOcean server. Our backend will query the database and create/update/delete new documents as needed.

We decided to install this on our production server at DigitalOcean directly, as opposed to using Atlas or mLab, as this will give us faster, more direct access to our data. Should we need to scale the app, moving to an offsite service such as Atlas would not be too hard- as this is all coded in through `MONGO_URL` and `MONGO_AUTH` environment variables.

<br>
<br>

# 9. Explain the different high-level components (abstractions) in your App.

Our app is made up of five main components:

> 1. **Guest App.** Our server will serve the guest app for users who have not provided any authorization details. This app will have three main react components: AppRouter (with Navigation), SplashPage (for app information and to login) and ContactPage (for contact details).

> 2. **Employee App.** Our server will serve the employee app for users who provide employee authorization details.  This app will have three main react components: 
>  - AppRouter (with Navigation)
>  - DashboardPage (to view and submit timesheets) 
>  - SettingsPage (to update account details).

> 3. Manager App. Our server will serve the manager app for users who provide manager authorization details. This app will have five main react components: 
>  - AppRouter (with Navigation)
>  - ReportPage (to generate a report of timesheets)
>  - ApprovePage (to approve submitted timesheets)
>  - ManageEmployeesPage (to manage employees)
>  - SettingsPage (to manage business specific settings such as rate multipliers).

> 4. **Express Backend.** Our server will listen for requests, handle those requests, interact with our database, serve static assets, and serve data in JSON format. Our server will also do all the authentication and authorization work and we hope to implement a mailer.

> 5. **MongoDB Database.** Our database will act as the store for all the information we want to save. Thsi includes, user data, shift data and business data.

<br>
<br>

# 10. Detail any third party services that your App will use.

- **DigitalOcean** for hosting - This is a somewhat similar service to AWS or GCS, except it's a little simpler. Their pricing model is a lot more standardized and their model works on providing a server with SSH access, so there's less "Learning AWS" around the production process. We will need to SSH into this terminal and clone our `master` branch, then install dependencies and run from there.

- **MongoDB** for the database. This will also be installed on our production server, and run as a separate service.

- **Figma** for developing the wireframes. We had a two-stage design process- An initial group-planned mock wireframe, and then more fleshed-out "design" wireframes.

- **Trello** for general project management. We lean *heavily* on this! We've multiple boards for resources and internal info, but it all flows back to our main <a href="https://trello.com/b/DFlgggpu/scrum-board" target="_blank">Scrum</a> board.

- **Git** and **Github** for version control. See below for more detail about our Git workflow.

<br>
<br>

# 11. Identify the database to be used in your app and provide a justification for your choice.
We will use <b>MongoDB</b> for our database. The benefits are:
- Faster than SQL database

- Use less space

- Open source

- More flexible (no need pre-defined schema)

- Used by big companies (e.g. Expedia, Bosch, Otto, eBay, Gap, Forbes, Foursquare, Adobe, Intuit, Metlife, BuzzFeed, Crittercism, CitiGroup, the City of Chicago, others.)

<br>
<br>

# 12. Discuss the database relations to be implemented.
We will implement three relationships in our database:

- In every `employee` document, the `business` property is a reference to a `business` document. This is because every employee belongs to a business.

- In every `shift` document, the `employee` property is a reference to an `employee` document. This is because every `shift` belongs to an `employee`.
- In every `business` document, the `manager` property is a reference to a `manager` document. This is because every business belongs to a `manager`.

<br>
<br>

# 13. Provide your database schema design.

We have 4 mongodb Schemas for use in our app: `Employee`, `Manager`, `Shift`, and `Business`.

> -**Employee**  
> - id: String (Auto generated by mongoose)
> - firstName: String
> - lastName: String
> - email: String
> - password: String (hashed and salted value)
> - location: [ array of Strings ]
> - standardRate: Number (cents)
> - dateAdded: Date (Default: "now")

`employee` has no references. Their `location` is an array, selected on the frontend by pulling in the available options from `business`

> -**Manager**  
> - id: String (Auto generated by mongoose)
> - email: String
> - password: String (hashed and salted value)
> - business: [ references `business` `id` ]
> - dateAdded: Date (Default: "now")

`business` references the ID of `business`, tying the manager to the business

> -**Shift**  
> - id: String (Auto generated by mongoose)
> - employee: [ references `employee` `id` ]
> - date: Number
> - location: [ Array of Strings ]
> - startTime: Number
> - endTime: Number
> - standardMinutes: Number
> - overtimeMinutes: Number
> - doubleTimeMinutes: Number
> - totalPay: Number (cents)
> - status: String ('pending', 'approved', 'rejected', 'removed')
> - dateAdded: Date (Default: "now")

`employee` references the ID of `employee`, as each shift is owned by an employee

> -**Business**  
> - id: String (Auto generated by mongoose)
> - name: String
> - address: String
> - locations: [String]
> - overtimeMultiplier: Number
> - doubleTimeMultiplier: Number
> - manager: [ Array, referencing `manager` `id`s ]
> - dateAdded: Date (Default: "now")

`manager` references the ID of `manager`, to keep track of the managers tied to this business

<br>
<br>

# 14. Provide User stories for your App.
### User Profiles
We focussed on providing a number of basic user profiles based on the types of users we are likely to encounter. We were informed there are a number of students and graduates who are employed in the shops, and the managers vary in age, the youngest being 24. From this, we created some basic profiles, and decided to focus on how the app may be used rather than fleshing out too many details about the characters.

<img src="assets/images/user_stories/User_Profiles.png" width="250" align="top">

### User Stories(Employee)
Employee user stories helped us to really understand that the employee will be looking for a fast, quick, easy option. Nobody likes waiting around after their shift to fill in paperwork, and nobody wants many details stored on our service. Quick login, with a quick entry of shifts, and that's that. They're likely to be on mobile, so this will be a mobile first approach.

<img src="assets/images/user_stories/Employee_User_Story_1.png" width="250" align="top">

<img src="assets/images/user_stories/Employee_User_Story_2.png" width="250" align="top">

<img src="assets/images/user_stories/Employee_User_Story_3.png" width="250" align="top">

### User Stories(Manager)
This was where we realised the bulk of our app's features would take place. The main "employer" section requires us to make multiple pages for administration as well as information the employer can get out of the app. In the future, we'd love to add exporting/ integration into business management software, but for now we decided to focus on a "dashboard", web version first.

<img src="assets/images/user_stories/Employer_User_Story_1.png" width="250" align="top">

<img src="assets/images/user_stories/Employer_User_Story_2.png" width="250" align="top">

<img src="assets/images/user_stories/Employer_User_Story_3.png" width="250" align="top">

### Link To: **[User Stories Trello Board](https://trello.com/b/1kl5tgnk)**

<br>
<br>

# 15. Provide Wireframes for your App.

Wireframes were a 2-stage process for our group. A quick, dirty first pass, and then a more design-focussed second pass, later on. 

## Initial Wireframes

### Link To: **[First Pass Wireframes on Figma](https://www.figma.com/file/gQQXmtltA663KtTEjNjUGpPT/Wireframe)**

We started out wireframes once we had our user stories and general feature set down. We worked on these together, quite quickly, so as to give us a foundation as to what Architecture we would be looking at using. From there, we moved on to more specific design wireframes.

### **Guest Pages(LP)**
<img src="assets/images/wireframes/2018-07-11_Guest_Pages_wf.png" width="800" align="top">

### **Employee Pages**
<img src="assets/images/wireframes/2018-07-10_Employee_Pages_wf.png" width="800" align="top">

### **Manager Pages**
<img src="assets/images/wireframes/2018-07-10_Employer_Pages_wf_1.png" width="800" align="top">

<img src="assets/images/wireframes/2018-07-10_Employer_Pages_wf_2.png" width="800" align="top">

<img src="assets/images/wireframes/2018-07-10_Employer_Pages_wf_3.png" width="800" align="top">

### Link To: **[First Pass Wireframes on Figma](https://www.figma.com/file/gQQXmtltA663KtTEjNjUGpPT/Wireframe)**

## Design Wireframes

### Link to **<a href="https://www.figma.com/file/E6dEYafb0SWYjyU57uw4HRga/Chicken-in-Design">Design Wireframes on Figma</a>**

(I think it's worth noting here that whilst we all contributed to how we wanted this app to look and feel at a higher level, a lot of the credit for the main design implementation and styling choices credit to <a href="https://github.com/mcwinter07/little-bow-peep">Winter</a>, and his incredible eye. We worked on this as a team, provided feedback and guidance, but he's really gone above and beyond in turning these ideas into a beautiful design. Thanks, Winter! 👍)

### **Guest Pages**

We decided to implement a mobile-first design for our guest and employee login pages as they would be the most frequent users of the Chicken-in Web app. The single page design allows the users to rapidly digest the purpose of the app with a summary of its full functionality in the about section.

<a href="assets/images/guest-loginPage.png" target="_blank"><img src="assets/images/guest-loginPage.png" width="800"></a>

### **Employee View (Mobile First)**

Iterating on the single page design, Red Rocks employees are redirected to a lightweight rostering app with the immediate ability to add and review past/pending/rejected shifts. We found that this stripped back interface would best serve the needs of the client's team, who found their paper-based system inefficient and time-consuming.

<a href="assets/images/employee-pages.png" target="_blank"><img src="assets/images/employee-pages.png" width="800"></a>

## **Manager View (Desktop First)**

On successful manager login, the user is redirected to the manager dashboard, where they have access to several core functions of the app.

Managers will be able to view weekly shift reports, approve or reject pending shifts input by employees, manage their teams, stores and configure their business settings.

After our initial meeting with the client, our team decided that we could not integrate mobile-first design for the manager dashboard without sacrificing the ability to display and easily read shift data. As such, the manager dashboard was created with a desktop only view.

## **Manager Reports**

On this page, the manager is given an overview of the weekly shifts that have been approved or are pending approval. A stretch goal is to integrate a "print report" function that produces a print ready pdf for physical documentation. An additional consideration is to include data visualisation within this dashboard further support the reporting functionality.

<a href="assets/images/manager-reports.png" target="_blank"><img src="assets/images/manager-reports.png" width="800"></a>

## **Manager Approvals**

On this page, managers have the ability to view all pending shifts input from employees and approve/reject them. Stretch goals are to include a comment popup when rejecting a shift to give further clarification to an employee as to why the shift has been denied.

<a href="assets/images/manager-approvals.png" target="_blank"><img src="assets/images/manager-approvals.png" width="800"></a>

## **Manager Team Management**

We decided that a full-scale HR app that stored and protected large amounts of employee data was not necessary for our client scale. Designed for ease of use, we kept the interface lean, with the ability to quickly edit, remove (archive), and add new employees within one view.

<a href="assets/images/manager-teamManagement.png" target="_blank"><img src="assets/images/manager-teamManagement.png" width="800"></a>

Upon submitting, a new employee will be registered to the email input with a default password given. This can be changed at any point by the employee to create a secure login that they alone will know.

<a href="assets/images/manager-teamManagement-newEmp.png" target="_blank"><img src="assets/images/manager-teamManagement-newEmp.png" width="800"></a>

## **Manager Settings**

Rather than hard code the values for overtime and double time, we decided to give our client the option to change the multiplier according to the current award rate in hospitality, as this is prone to change.

<a href="assets/images/manager-settings.png" target="_blank"><img src="assets/images/manager-settings.png" width="800"></a>


### Link to **<a href="https://www.figma.com/file/E6dEYafb0SWYjyU57uw4HRga/Chicken-in-Design">Design Wireframes on Figma</a>**


<br>
<br>

# 16. Describe the way Tasks are being allocated and tracked in your project.

### Link To **[Main Scrum Trello Board](https://trello.com/b/DFlgggpu)**

Task tracking and breaking out tasks to individual features was really important to our team dynamic. Early on, we had very frank and open discussions about the fact that we had a diverse team, with varying levels of time outside of class and confidence in abilities. We decided to work hard to implement agile practices and break down tasks into achievable chunks, so as to best work together to achieve our goals.

To that end, from the outset we implemented a main Scrum-style Trello board, split into a number of sections:

<a href="assets/images/scrum.png" target="_blank"><img src="assets/images/scrum.png" width="800"></a>

### Link To **[Main Scrum Trello Board](https://trello.com/b/DFlgggpu)**

### Ideas / Stretch Goals
> All our ideas started here - straight from our very first planning session after our initial client brief. New ideas land here first, are discussed and formed if agreed to, where they move to “Tasks”.

### Tasks
> All our main work starts here, first. ‘Tasks’ are usually larger chunks of work, including documentation, planning, and research as well as the obvious “App Feature” tasks. If necessary (mostly during development), these Tasks will be broken down into smaller “Features”, where they can be worked on by individuals. An example might be “User System (Model, Login, Logout, Auth)”

### Features
> Mostly used in the Development stage, “Features” are generally front or back-end pieces of code, that come together to make one functional piece of the App. An example might be “Frontend: User Login Form”

### To-Do (Next Few Days)
> The title is fairly self-explanatory, this is just a staging area for us to further breakdown our workflow. From here, we’ll decide at standup meetings who is going to work on which card.

### In Progress
> Self-explanatory- This is where we’ll hold the cards we’re currently working on. No card gets here without assigning a team member to it.

### Blocked
> If something is holding us up from work, we put the card here, and comment as to what the blocker is. The intention here is for us to help one another overcome the blockage, or rethink the card scope or timing.

### Pending Review
> Somewhere to put cards if we need another team member to check on the work or review the code.

### Completed
> Completed cards go here! Yay! 

### Access / Resources
> A collection of links we can use to quickly get around.

The board is designed to be self-documenting, and make sense, so as not to be too confusing. We decided against using many, smaller boards, in favour of one large board, where we can follow a card from original idea through to completion.

<br>
<br>

# 17. Discuss how Agile methodology is being implemented in your App.

From the outset of this project, we decided to take a lot from the Agile methodology. Given that each of us has our own unique strengths, we have embraced the idea that we will be far more powerful as a team, and the Agile (Specifically, Scrum) practices offer a lot in the way of organization. 

### Agile Practices Included:
- Scrum Board (See Scrum section for breakdown)
- StandUp Meetings
- Ideation sessions (multiple for design, architecture, initial planning)
- Review (Retro)
- Code Reviews

### Ideation
<a href="assets/images/ideation.jpg" target="_blank"><img src="assets/images/ideation.jpg" width="800"></a>

We kicked it off with a big Ideation whiteboard session. This was great in laying out what we needed and wanted to achieve given the client’s needs. Further meetings were had later in this vein for the Architecture section, and again for Design. Iterations continued with each meeting, and the product started to take form. From this, we started up our Trello board “Ideas” column, and the flow progressed from there.

<a href="assets/images/ideation2.jpg" target="_blank"><img src="assets/images/ideation2.jpg" width="400"></a> <a href="assets/images/postit.jpg" target="_blank"><img src="assets/images/postit.jpg" width="400"></a>

(We also had fun. Winter got *really* into his post-it notes :D)

### StandUps
We also agreed to daily stand-ups, so as to get one another on the same page as far as what we’re all working on. We had some big conversations about our plans to break down tasks and work together. We all agreed that whilst it’s important to lean on our strengths, nobody should have to feel as if they are “Carrying” any aspect of the project - from design, through to code. To this end, regular stand-ups, and breaking things down into achievable chunks were very important to all of us. 

### Blocked / Review
Adding in a “Blocked” step to the scrum board was another big part of this. We agreed that if something’s holding us up, we can park the card here and move on to something else, after notifying the team or finding someone to help. We plan to hold weekly reviews- Perhaps not full “retrospectives”, as we may not have time, but at the very least borrow from the “safe, blameless space” ethos while holding these reviews.  

As far as Timeline planning goes, we have begun to track our progress using Maxi’s previously made Timeline Tracker app! 

### Timeline Planning
<a href="assets/images/timeline.png" target="_blank"><img src="assets/images/timeline.png" width="800"></a>

This was actually really useful! It was really impressive and empowering to see how we could actually use a tool that was previously made by one of our own, to further our project needs. Thanks, Maxi! 

### Meetings

Our initial client contact was Maxi, who is friends with the business owner's Son (One of the managers at the stores). His initial dealings were with the son, and eventually moved on to Ed, the owner. Meetings were held with Ed about initial ideas and planning, and again when we'd thought about our options and what to present to him- where we discussed the plans in more detail. 

We queried him about branding and he wasn't overly across the concept. He mentioned Red for a colour and the Chicken Logo on his stores - Though when we googled these logos we saw them to be inconsistent. Winter made a new, custon `Chicken-In` Logo, and Ed was reportedly very impressed.

<br>
<br>

# 18. Provide an overview and description of your Source control process.

For version and source control, we will be using Git, with a main repository stored on Github. At this early stage we’ve planned to use a “Protected” `master` branch for pushing to production, and a `develop` development branch for working between releases. 

We have taken a lot of inspiration from this model: https://nvie.com/posts/a-successful-git-branching-model/ 

Master (Protected): The `master` branch is ‘Protected’ against any `git push` commands, and only able to be merged via Pull Request on Github. The idea behind this is that `master` is only to be used for stable releases that have been tested and checked thoroughly.

For individual features, Our plan is to use separate `feature` branches cloned off of the `develop` branch. These branches will be merged into the `develop` branch, after changes are pulled and conflicts resolved. We intend to push these `feature` branches as well, to keep a record of our progress, though this isn’t really necessary for a project of this scale.

## **Creating a feature branch (Example, “Login Form”)**

#### Step 1: Make sure you’re in ‘develop’

> `git checkout develop`

#### Step 2: Pull the changes from the main repo, getting you up to date

> `git pull origin develop`

#### Step 3: Create your new feature branch - This is important! Otherwise we’ll be conflicting up the wazoo on develop :P And try to name your branch smart! Use the name on the Trello card you’re working on, if possible.

> `git checkout -b login-form develop`

> (note the ‘develop’ on the end, makes sure it creates the branch off of ‘develop’, not ‘master’)

#### Step 4: Make your changes! Do your code!

> <-- 🎉  -->

#### Step 5: Add and commit your changes to your branch

> `git add .`

> `git commit -m “A descriptive and useful commit message please!”`

#### Step 6: Push your branch to github (for history's sake)

> `git push origin login-form`

#### Step 7: Change back to ‘develop’

> `git checkout develop`

#### Step 8: Do a git pull (on ‘develop’ branch) - this is to make sure that if someone else has gone ahead and pushed since you last worked on it, you’re all up to speed. *ALWAYS GIT PULL BEFORE PUSH! :D*

> `git pull -u origin develop`

> (or just `git pull` if you’ve already set your upstream)

#### Step 9: Merge your branch back in (Again: Don’t forget to pull, first!)

> `git merge --no-ff login-form develop`

#### Step 10: Push your change to develop

> `git push origin develop`

<br>
<br>

### Git Workflow Thus Far
<a href="assets/images/git-workflow.png" target="_blank"><img src="assets/images/git-workflow.png" width="800"></a>

Git workflow using these methods so far has been good. There are a lot of erroneous 'merge commits', but this is fine- We've been using them to track branches when necessary. At at least one occasion `oheydrew`(Drew) forgot to push up his work, but since he'd done it in a side branch, he just pulled the latest from `origin`, and merged in his previously completed branch. A simple example of how useful branches can be!

<a href="assets/images/github-branches.png" target="_blank"><img src="assets/images/github-branches.png" width="800"></a>

We've been pushing branches to Github, though we can see there will end up being quite a few branches there if we do so. In the future, this may slow to more stable release features. 

<br>
<br>

# 19. Provide an overview and description of your Testing process.

We plan to implement two types of tests: 

- **Unit Tests**:  To test functions and components
- **Integration Tests**: To 'black box' test functionality of our code as a whole

We plan to integrate Jest for our main Test suite, as well as Enzyme to test React components. Tests for React components will live inside a /test/ subfolder inside the component folder itself.

For known and pre-designed code components, we plan to implement some level of T.D.D, writing tests before code, to garauntee that the code functions as planned. In cases where more inventive code solutions are required, we will implement tests for these functions retroactively.

Integration Testing will mostly happen on the backend and will be used to test database and model data, as well as larger function chains. 

We have extended goals to integrate Continuous Integration using TravisCI - This would enable us to be able to automatically run tests, before deploying to our `master` branch. This may or may not get implemented, depending on how complete the project gets.

<br>
<br>

# 20. Discuss and analyse requirements related to information system security.
Managers will need to be confident that only they can access their account, manage employees and approve employee timesheets. Employees will need to be confident that only they can submit their own time sheets. We will facilitate this by implementing server-side authorization and authenticantion.

Tokens will be bundled up inside Cookies (Not LocalStorage), and inside the cookie, along with the valid email address, will be a flag: `userType`. This will be either `employee` or `manager`, and will allow our cookieparser to get this user type and check the email credentials against the correct user database. This is still secure, as the cookie/token will need to be valid for this checking to occur, and cookies will only be handed out in the event of a successful login. 

If a manager wishes to also fill out their own timesheets, they will be required to log out as a manager, in this system. This is regrettable, but given the scope of what we can achieve, we decided this a fair compromise. 

As always, with cookies, if a malicious script or other method were to steal the cookie from somebody's browser, they would be able to get access to the site. But this is the case with many cookie based login systems, and can't be helped. We plan to minimize this by implementing short-expiry times on cookies (especially on the manager end). This will require more logins, but is worth it for the additional security benefits.

<br>
<br>

# 21. Discuss methods you will use to protect information and data.
One of the key ways we plan to secure information, is not to store irrelevant data at all. This is a system which tracks hours and overtime, not employee information. As such, only the first and last name of the employee is stored, and minimal business information. Nevertheless, the hours and pay rates of employees is stored with identifiable information, as such, we need to take security seriously.

We will implement a login endpoint that checks the incoming login details against details stored in the database. The server will then create a JWT and provide it to that user via a private cookie.  Additionally, we will protect all our api endpoints with middleware that will check requests for a JWT. If a valid JWT is not provided, the server will return a status of 401. If a valid JWT is provided, the server will handle the request appropriately. We will also implement a logout endpoint that will remove the JWT from the user's cookie. Additionally, we will avoid storing authorization data in local storage, and we will also hash incoming passwords before storing them in the database.

<br>
<br>

# 22. Research what your legal obligations are in relation to handling user data.
Under Australian Privacy laws, we are required to safeguard any user information that we collect and store. We have the responsibility to protect users' personal information from theft, misuse, interference, loss, unauthorized access, modification and disclosure. We must also take reasonable steps to destroy or de-identify personal information when it is no longer needed. Personal information can include name, signature, address, email, telephone number, date of birth, medical records, bank account details, etc.