# Project Intent & High-Level Overview

The Frame allocation tool is, at a high level, a Ruby on Rails back-end project with a JavaScript React Frontend incorporating Redux for state management. Additionally, this project has an API built in JavaScript that sends queries to, and receives data from, a connected tabular model using the Microsoft DAX query language. Without this API, data doesn’t really come into the application.

The application has a few primary features:
- Make search selections to Allocate data 
- Update allocations and submit them over sftp
- Save working allocations 
- Load working allocations 
- Load submitted allocations 
- Upload Manual Allocations 
- Upload Store to Store Transfers 
- Upload RMA Transfers 
- Upload Min Max Files 
- Modify Store groups 
- Activate/deactivate stores 

## Current App Service

- [https://frameprod.azurewebsites.net](https://frameprod.azurewebsites.net)

## Visual Studio 

- [https://shroodbi.visualstudio.com/Frame%20Allocation%20App](https://shroodbi.visualstudio.com/Frame%20Allocation%20App)

## Repository Link

- [https://shroodbi.visualstudio.com/Frame%20Allocation%20App/_git/Frameco_git](https://shroodbi.visualstudio.com/Frame%20Allocation%20App/_git/Frameco_git)

## Associated Azure Services

## Branch Naming and Process

Note the naming convention for this app is X.XXA ascending (current version as of writing this is 1.97d). When updating the app, a new branch should be created with an updated name, notes should be added top Readme.md, and then the current version number should be updated.

## Adding a user

To add a user, create a new user on the users table with a relevant email address, and add that user to the active directory client.

## Auxiliary Services

- Webhook processing
- Status checks
- SFTP connection
- SSH [https://frameprod.scm.azurewebsites.net/webssh/host](https://frameprod.scm.azurewebsites.net/webssh/host)

## Environment Variable Notes & Container Registry Deployment Credentials

Environment Variables & Docker Deployment.

- [https://shrood.sharepoint.com/:w:/r/_layouts/15/Doc.aspx?sourcedoc=%7B5BAB7A21-5DDC-408F-949E-F69E2BDE9E54%7D&file=Credentials%20and%20Environment%20Variables%20-%20Frame%20Allocation.docx&action=default&mobileredirect=true](https://shrood.sharepoint.com/:w:/r/_layouts/15/Doc.aspx?sourcedoc=%7B5BAB7A21-5DDC-408F-949E-F69E2BDE9E54%7D&file=Credentials%20and%20Environment%20Variables%20-%20Frame%20Allocation.docx&action=default&mobileredirect=true)

## Relevant App Service Features

## Project Setup

You will need some version of Ruby installed, and this project should be run in a Unix/Linux environment. Ruby version numbers are outlined in the `.ruby-version` file in the root directory.

You will also need to have Node installed. The Node version will be specified in the `package.json` file in the root directory. You will also need NPM/yarn to run the application. I recommend using Yarn.

For both opf these together, it is recommended to use [ASDF](https://github.com/asdf-vm/asdf-ruby) follow install instructions for asdf for your particular environment, install ruby and nodejs plugins, and set versions to 2.7.4  for ruby and 16.18.0 for nodejs.

You will need to run the following prior to installing ruby 2.7.4:

`sudo apt-get install -y libssl-dev zlib1g-dev`
`sudo apt-get install build-essential`
`sudo apt-get install libc6-dev`

To run the project locally, you will need to run `bundle install` to add rails dependencies. You will also need to install FreeTDS in your environment. You may need other dependencies, so you’ll need to troubleshoot as necessary. If `bundle install` fails look at error outputs and try and determine what is missing. Most of these local dependencies are from the need to connect to Microsoft SQL.
You will likely run into an issue with tiny_tds requiring FreeTDS.
[possible solution](https://github.com/rails-sqlserver/tiny_tds/issues/508)

Additionally, you will need to run `yarn install` for the included lockfile (yarn.lock) you will need to make sure you have yarn installed globally. There is not an equivalent package-lock.json.

Once both `yarn install` and `bundle install` have succeeded, you will need to open a terminal and run `rails s` to start the Rails development server, and a second terminal with `yarn run webpack` to start webpack for development in the frontend. Running webpack in development mode allows for a quick refresh.

---

## Project Section Notes

**App**: this is the backend folder. This folder has everything pertaining to Rails, controllers, etc.

- `App/javascripts`: most important thing in here will never be modified by the user (bundle files)
- `App/stylesheets`: All stylesheets present for the app in SCSS. I recommend using search in your editor to find classes. Tailwind is not in use on this application.

- `App/controllers`: This is where all the controllers that connect to the database reside. Fetches to the cube are handled on the frontend, but all DB queries happen here.

- `Api/controllers/api`: Most controllers to specific tables present in API routes.

- `App/helpers`: Not really used in this project.

- `App/jobs`: Not really used in this project.

- `App/mailers`: Only used within the context of the webhooks monitoring. There is a cron job that happens that checks tables that are frequently updated via webhooks to make sure they’ve been updated.

- `App/models`: Not much here. Generally a space for adding additional class methods to DB models, but not heavily utilized in this project.

- `App/views`: This is an important area of the application. Much like in the controllers where one needs to ensure that parameters are permitted, the views level needs to have appropriately structured jbuilder files that translate DB requests into JSON usable by the frontend. There is generally a 1:1 mapping between DB tables here, but keep an eye out.

- `App/config`: Also important. `Database.yml` file lives here, someF credentials live here, OAuth environment variables, sftp and SMTP environment variables, etc. Relevant environment variables are outlined in the environment variables file, but keep an eye on this section.

**Frontend**:

- `Frontend/actions`: This houses all THUNK redux actions. It may be useful to at some point refactor to use a newer version of Redux, but this isn’t a small undertaking, so for the time being thunk actions (primarily) live here. Again, there is generally a 1:1 mapping between DB tables, APIs, and routes, with some exceptions.

> **Note**: The most useful way to begin understanding this state is by starting the server locally, running the app in development mode (`yarn run webpack`), and then examining the state through opening up the console in your browser and typing `window.getStateObj()`. You can also use Redux dev tools.

- `Frontend/components`: All react components live here. Most have a component page and a container page to wrap the redux state. Sometimes this is present in the component page itself.

- `Frontend/components/active_store_page`: Admin control for which stores will be rendered in the app/are searchable.

- `Frontend/components/calculation_settings_page`: Navigation page to set the calculation settings for the current allocations.

- `Frontend/components/dax_query_page`: Test page for running sample DAX queries while connected to the cube. Useful for syntax.

- `Frontend/components/dropdown`: Different dropdowns used within the app. Mainly navigational.

- `Frontend/components/edit_storegroups`: Less useful component for editing store groups. Frame doesn’t appear to use this function much.

- `Frontend/components/header`: Application header.

- `Frontend/components/loader`: Loading components.

- `Frontend/components/main_page`: Login page.

- `Frontend/components/min_max_page`: This should be used as the basis for the updated initials functionality. See 1.98 build branch for relevant cloned state and components. You will still need to work on DB models/functionality for the main table functions. Interface for editing min max_page.

- `Frontend/components/modal`: A collection of modals. Much functionality is included here, please review individually in the code. Things like uploads, submitting an allocation, etc, are all present here.

- `Frontend/components/product_selection_page`: The main selection page for products. This determines search criteria.

- `Frontend/components/results_page`: This contains results pages for the allocation as well as results pages for saved allocations and working allocations. Each should be examined independently, although they have a similar structure.

- `Frontend/components/search_bar`: This is a relatively simple component that houses buttons for navigation and search.

- `Frontend/components/store_selection_page`: This component is used for selecting stores in the application.

- `Frontend/components/table_functions`: This component houses various functions related to the table functionalities.

- `Frontend/reducers`: Redux reducers for state. The whole state shape is constructed from this folder.

- `Frontend/reducers/fco_memberships`: Store group memberships: relational reducer.

- `Frontend/reducers/fco_storegroups`: Store groups: grouped stores.

- `Frontend/reducers/fco_stores`: Individual stores.

- `Frontend/reducers/search_params`: Current search parameters.

- `Frontend/reducers/search_results`: Current search results.

- `Frontend/reducers/search_selectors`: Combination of possible selectors based on different available product selectors.

- `Frontend/reducers/store_weights`: Weighted values of stores based on sales. This is used in the computation of the ratios in the output of the allocation app.

- `Frontend/reducers/tabular_bulk_reducer`: Available bulks.

- `Frontend/reducers/tabular_style_reducer`: This reducer is related to styles in tabular data.

- `Frontend/reducers/transfer_records`: This reducer manages transfer records.

- `Frontend/reducers/ui`: This is used to determine which modals are active. Some modals use this, alerts however tend to use sweetalert2. It should be apparent from the code which is using which.

- `Frontend/store`: This is the function that generates the store which is then rendered and applied to the root component in `otb.jsx`.

- `Frontend/tests`: This is where frontend test should live.

- `Frontend/util`: This is where the frontend APIs live. Again, there tends to be a 1:1 relationship between these and the actions/tables/etc.

- `Frontend/App.js`: This is the main App component.

- `Lib`: The only relevant file in here is the `microsoft_graph_auth.rb` file. This pertains to Active Directory authentication.

- `Log`: These files are for the most part only relevant in production. However, they should be cleared out before building/pushing a build. In production, they will be updated as different actions happen. Additionally, they should be copied into the SFTP before a new build is pushed so there is a record of logs.

- `Dockerfile`: This is the set of instructions for Docker. Important features are SSH and preinstalling dependencies like FreeTDS.

**Notable Dependencies**:

- FreeTDS
- Tabulator-tables
- Sweetalert2
- React-beautiful-dnd

**MIN_MAX UPDATE!**  

Every once in a while there is a massive min_max update that needs to take place. This is that process:

- [https://shrood.sharepoint.com/:w:/r/_layouts/15/Doc.aspx?sourcedoc=%7B202EE971-D2F6-4C82-894B-B5956B9EA9EB%7D&file=Min-Max-Bulk-Upload.docx&action=default&mobileredirect=true](https://shrood.sharepoint.com/:w:/r/_layouts/15/Doc.aspx?sourcedoc=%7B202EE971-D2F6-4C82-894B-B5956B9EA9EB%7D&file=Min-Max-Bulk-Upload.docx&action=default&mobileredirect=true)
