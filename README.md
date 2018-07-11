# 1. Who is your client?
Our client, Edwin Huang, owns and operates a number of charcoal chicken shops around Victoria, under the brand name “Red Rocks Charcoal Chicken”. He splits his time between working in the stores as a manager, and doing all the administrative/entrepreneurial work as the owner.

# 2. What is your client’s need (i.e. challenge) that you will be addressing in your project?
One of Edwin’s biggest challenges is keeping track of employee hours worked, calculating overtime and calculating how much he owes in wages to each employee. Currently, his employees record how many hours they’ve worked on a paper form, and he manually updates his excel spreadsheet at the end of the week. It’s time consuming work and his employees often make mistakes which means he has to manually follow up with those employees to clarify the situation.

# 3. Describe the client’s current setup and data.
Red Rocks Charcoal Chicken does not currently implement a digital solution to this problem. They are currently using an excel spreadsheet to manage employee data and employee expenses. The managers of each store must manually update the spreadsheet at the end of every week- This is time consuming and could better be handled through the use of an app and database solution.

> **Talk about data structure**

# 4. Describe the project will you be conducting and how your App will address the client’s needs.
We will develop an online app that will enable Ed’s employees to easily enter in the amount of hours they’ve worked. The app will automatically calculate the standard and overtime hours based on the information, and display this information on a dashboard that Ed can view. Ed can add/remove employees from the system and review the submissions before approving them. The dashboard will also include an overview of past wages paid, which he filter by various fields (dates, locations, employee, etc).

This app will streamline the process of calculating wages, reduce the number of errors and remove the need to manually update an excel spreadsheet.

# 5. Identify and describe the software (including databases) to be used in your App.

### Frontend:
We will develop the frontend in JavaScript, using the React library. We will also use react-router to enable client-side routing and Webpack as our asset budnler.

### Backend:
We will develop the backend in JavaScript, using the express library to speed up the process. 

### Database: 
We will use MongoDB for our database. The plan is to install our database on the server, as opposed to using a third-party database manager like Atlas or mLab.  We'll use the mongoose library to interact with our database.

### Host:
We will use DigitalOcean to host our App.

# 6. Identify and describe the network setup you will use in your development.

Our app will live in a DiginalOcean virtual computer. Users will enter the domain name, chicken-in.com, into their browser and the server will handle their requests, serve them static assets and serve them data in JSON format. Users will interact with our app entirely on the browser.

# 7. Identify and describe the infrastructure (i.e. hardware) that your App will run on.

We will host our App on Digital Ocean. We will buy the cheapest plan, which gives us access to a virtual computer with 1GB of memory, 1vCPU, 25GB of SSD storage, and allow up to 1TB of transfers per month. We are planning to install our database on the server, so will not need to use third-party services like Atlas or mLab.

# 8. Describe the architecture of your App.

### Frontend:

We will create three seperate frontend apps. One for guest users, one for employee users, and one for the manager users. Our server will serve these apps to the user, depending on the authorization details they provide. Each app will utilise react-router to enable client-side routing within each app. These frontend apps will comminucate with our backend server via api requests.

### Backend:

We will run server.js on our DigitalOcean virtual computer. Our server will listen for requests and handle them according to the endpoints that the requests go to. Our server will serve all the static files to the user, depending on the authorization details they provide.

### Database:

We are planning to install a MongoDB database on our DigitalOcean server. Our backend will query the database and create/update/delete new documents as needed.

# 9. Explain the different high-level components (abstractions) in your App.

Our app is made up of five main components:
1. **Guest App.** Our server will serve the guest app for users who have not provided any authorization details. This app will have three main react components: AppRouter (with Navigation), SplashPage (for app information and to login) and ContactPage (for contact details).

2. **Employee App.** Our server will serve the employee app for users who provide employee authorization details. This app will have three main react components: AppRouter (with Navigation), DashboardPage (to view and submit timesheets) and SettingsPage (to update accoutn details).

3. Manager App. Our server will serve the manager app for users who provide manager authorization details. This app will have five main react components: AppRouter (with Navigation), ReportPage (to generate a report of timesheets), ApprovePage (to approve submitted timesheets), ManageEmployeesPage (to manage employees), SettingsPage (to manage account settings).

4. **Express Backend.** Our server will listen for requests, handle those requests, interact with our database, serve static assets, and serve data in JSON format. Our server will also do all the authentication and authorization work and we hope to implement a mailer.

5. **MongoDB Database.** Our database will act as the store for all the information we want to save. Thsi includes, user data, shift data and business data.

# 10. Detail any third party services that your App will use.

- **DigitalOcean** for hosting
- **MongoDB** for the database
- **Figma** for developing the wireframes
- **Trello** for general project management
- **Git** and **Github** for version control

# 11. Identify the database to be used in your app and provide a justification for your choice.
We will use <b>MongoDB</b> for our database. The benefits are:
- Faster than SQL database
- Use less space
- Open source
- More flexible (no need pre-defined schema)
- Used by big companies (e.g. Expedia, Bosch, Otto, eBay, Gap, Forbes, Foursquare, Adobe, Intuit, Metlife, BuzzFeed, Crittercism, CitiGroup, the City of Chicago, others.)

# 12. Discuss the database relations to be implemented.
We will implement three relationships in our database:

- In every employee document, the business property is a reference to a business document. This is because every employee belongs to a business.
- In every shift document, the employee property is a reference to an employee document. This is because every shift belongs to an employee.
- In every business document, the manager property is a reference to a manager document. This is because every business belongs to a manager.

# 13. Provide your database schema design.

```javascript
const managerSchema = 
{
  id: String,
  email: String,
  password: String
}

const employeeSchema = {
  id: String,
  name: String,
  email: String,
  password: String, // randomly generate a password upon creation and send emial to employee
  location: [ String ],
  standardRate: Number, // cents
  overtimeOneRate: Number, // cents
  overtimeTwoRate: Number, // cents
  business: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Business'
  }
}

const shiftSchema = 
{
  id: String,
  employee: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Employee'
  },
  date: Number,
  location: String,
  startTime: Number,
  endTime: Number,
  standardMinutes: Number,
  overtimeOneMinutes: Number,
  overtimeTwoMinutes: Number,
  totalPay: Number, // cents
  status: String
}

const businessSchema = {
  name: String,
  address: String,
  locations: [String],
  manager: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Manager'
  }
}
```

# 14. Provide User stories for your App.
### User Profiles
<img src="assets/images/user_stories/User_Profiles.png" width="250" align="top">

### User Stories(Employee)
<img src="assets/images/user_stories/Employee_User_Story_1.png" width="250" align="top">
<img src="assets/images/user_stories/Employee_User_Story_2.png" width="250" align="top">
<img src="assets/images/user_stories/Employee_User_Story_3.png" width="250" align="top">

### User Stories(Manager)
<img src="assets/images/user_stories/Employer_User_Story_1.png" width="250" align="top">
<img src="assets/images/user_stories/Employer_User_Story_2.png" width="250" align="top">
<img src="assets/images/user_stories/Employer_User_Story_3.png" width="250" align="top">

Link To: [User Stories Trello Board](https://trello.com/b/1kl5tgnk)

# 15. Provide Wireframes for your App.
## Initial Wireframes

### Guest Pages(LP)
<img src="assets/images/wireframes/2018-07-11_Guest_Pages_wf.png" width="800" align="top">

### Employee Pages
<img src="assets/images/wireframes/2018-07-10_Employee_Pages_wf.png" width="800" align="top">

### Manager Pages
<img src="assets/images/wireframes/2018-07-10_Employer_Pages_wf_1.png" width="800" align="top">
<img src="assets/images/wireframes/2018-07-10_Employer_Pages_wf_2.png" width="800" align="top">
<img src="assets/images/wireframes/2018-07-10_Employer_Pages_wf_3.png" width="800" align="top">

## Design Wireframes
> TBC 

Link To: [Wireframe on Figma](https://www.figma.com/file/gQQXmtltA663KtTEjNjUGpPT/Wireframe)

# 16. Describe the way Tasks are being allocated and tracked in your project.

## [Main Scrum Trello Board](https://trello.com/b/DFlgggpu)

Task tracking and breaking out tasks to individual features was really important to our team dynamic. Early on, we had very frank and open discussions about the fact that we had a diverse team, with varying levels of time outside of class and confidence in abilities. We decided to work hard to implement agile practices and break down tasks into achievable chunks, so as to best work together to achieve our goals.

To that end, from the outset we implemented a main Scrum-style Trello board, split into a number of sections:

<a href="assets/images/scrum.png" target="_blank"><img src="assets/images/scrum.png" width="800"></a>

Link To: [Main Scrum Trello Board](https://trello.com/b/DFlgggpu)

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

# 17. Discuss how Agile methodology is being implemented in your App.

From the outset of this project, we decided to take a lot from the Agile methodology. Given that each of us has our own unique strengths, we have embraced the idea that we will be far more powerful as a team, and the Agile (Specifically, Scrum) practices offer a lot in the way of organization. 

<a href="assets/images/ideation.jpg" target="_blank"><img src="assets/images/ideation.jpg" width="800"></a>

We kicked it off with a big Ideation whiteboard session. This was great in laying out what we needed and wanted to achieve given the client’s needs. From this, we started up our Trello board “Ideas” column, and the flow progressed from there.

<a href="assets/images/ideation2.jpg" target="_blank"><img src="assets/images/ideation2.jpg" width="400"></a> <a href="assets/images/postit.jpg" target="_blank"><img src="assets/images/postit.jpg" width="400"></a>

(We also had fun. Winter got *really* into his post-it notes :D)

We also agreed to daily stand-ups, so as to get one another on the same page as far as what we’re all working on. We had some big conversations about our plans to break down tasks and work together. We all agreed that whilst it’s important to lean on our strengths, nobody should have to feel as if they are “Carrying” any aspect of the project - from design, through to code. To this end, regular stand-ups, and breaking things down into achievable chunks were very important to all of us. 

Adding in a “Blocked” step to the scrum board was another big part of this. We agreed that if something’s holding us up, we can park the card here and move on to something else, after notifying the team or finding someone to help. We plan to hold weekly reviews- Perhaps not full “retrospectives”, as we may not have time, but at the very least borrow from the “safe, blameless space” ethos while holding these reviews.  

As far as Timeline planning goes, we have begun to track our progress using Maxi’s previously made Timeline Tracker app! 

<a href="assets/images/timeline.png" target="_blank"><img src="assets/images/timeline.png" width="800"></a>

This was actually really useful! It was really impressive and empowering to see how we could actually use a tool that was previously made by one of our own, to further our project needs. Thanks, Maxi! 

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

# 19. Provide an overview and description of your Testing process.

We plan to implement two types of tests: 

- **Unit Tests**:  To test functions and components
- **Integration Tests**: To 'black box' test functionality of our code as a whole

We plan to integrate Jest for our main Test suite, as well as Enzyme to test React components. Tests for React components will live inside a /test/ subfolder inside the component folder itself.

For known and pre-designed code components, we plan to implement some level of T.D.D, writing tests before code, to garauntee that the code functions as planned. In cases where more inventive code solutions are required, we will implement tests for these functions retroactively.

Integration Testing will mostly happen on the backend and will be used to test database and model data, as well as larger function chains. 

We have extended goals to integrate Continuous Integration using TravisCI - This would enable us to be able to automatically run tests, before deploying to our `master` branch. This may or may not get implemented, depending on how complete the project gets.

# 20. Discuss and analyse requirements related to information system security.
Managers will need to be confident that only they can access their account, manage employees and approve employee timesheets. Employees will need to be confident that only they can submit their own time sheets. We will facilitate this by implementing server-side authorization and authenticantion.

# 21. Discuss methods you will use to protect information and data.
We will implement a login endpoint that checks the incoming login details against details stored in the database. The server will then create a JWT and provide it to that user via a private cookie.  Additionally, we will protect all our api endpoints with middleware that will check requests for a JWT. If a valid JWT is not provided, the server will return a status of 401. If a valid JWT is provided, the server will handle the request appropriately. We will also implement a logout endpoint that will remove the JWT from the user's cookie. Additionally, we will avoid storing authorization data in local storage, and we will also hash incoming passwords before storing them in the database.

# 22. Research what your legal obligations are in relation to handling user data.
Under Australian Privacy laws, we are required to safeguard any user information that we collect and store. We have the responsibility to protect users' personal information from theft, misuse, interference, loss, unauthorized access, modification and disclosure. We must also take reasonable steps to destroy or de-identify personal information when it is no longer needed. Personal information can include name, signature, address, email, telephone number, date of birth, medical records, bank account details, etc.