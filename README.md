#Github Action to Github Pages 


Create react app 

- Create folder with your app name 
- open it with cmd or gitbash
if you are using npm (node pakage manager.
- type npx create-react-app .
------> (note write this command if you have create a folder already on your system (Incase you did not created any folder yet follow the below given instruction )
--> for creating react app with app folder
--> Open your cmd by typing cmd on search bar of windws 
and type :
npx create-react-app Name_of_Your_App

Creating Github Repositry 
Now Create Go to Your Github  and create a repositry with same name to recoagnize easily
Push Your code to github repo you have created by uing this commands 

Opening App Directory (Easiy Method)

- Open the folder of your app and click header bar which is showing your path of your system;
- do not delete the path but just click and type cmd
you will in the that directory easily ->
or 
get out of folder of your app and right click on it by holding shift button (first press shif and hold and right click on your app folder ) you will gitbash option or open with powershell click on it.
your directory will be open 

Now Push Code to master branch :
1. check status of your app:
 run command in you cmd : git status
2. initilize the repositry 
 run command in your cmd: git init
3. now adding the changes
 run command in you cmd : git add .
2. commit the changes  
 run command in your cmd: git commit -m "my first commit"
3. now go to your repositry and copy the repositry link (HOW YOU WILL DO THAT ---> GO YOUR REPOSITRY AND ON RIGHTHAND SIDE YOU WILL FIND THE BUTTON WITH GREEN COLOR OF DROPDOWN WHICH SAYS "CODE" CLICK ON IT AND COPY THE HTTPS: LINK

4. Now back to cmd  : run this command to add the path github cloud remote repositry:
run command  : git remote add origin "https://github.com/ikishorkumar/reactapp.git"
you have to replace the HTTPS url with your repositry URL

5.last to send this whole data to this repositry :
run command : git push -u origin master
here master is branch name you can use your branch i will suggest you us same



Create Workflow:
just go your github repositry and click on action tab it will automaticly the workflow for you but (we need node.js workflow ifit finds that the one with green logo of node it's just node.js (not the publish one) we need node.js one with green logo) select that one it will open a  yml file do nothing click on commmit on right handside setting will remain as defualt as it is :


Now click on your repositry go settings and go down to the github pages section you will find your site is hosted at the https : if not then just click the drop down which shows your branch name on top left hand side in row of code buttton just click on that dropdown
now type gh-pages  and hit enter 
done now go settings again and find the section of github pages you will see a link .
we will need that link first we will open our code with any code editor and open package.json and paste (  "homepage": "https://ikishorkumar.github.io/reactapp",
) it on top of this "name" : "your-app-name" : 
Now your file will look like this:
{  "homepage": "https://ikishorkumar.github.io/reactapp",
    "name" : "your-app-name",

->
now save this and open your cmd and run this command to install gh-pages
run commad : npm install --save gh-pages

now just open you package.json file again and add these two lines to secrets section: 
after this line of ejection     "eject": "react-scripts eject",
"predeploy": "npm run build",
"deploy": "gh-pages -d build"

and save it Now it comes the triky part : 
before pusing this data to git repositry you might pull the changes that you have done the git repositry :
open cmd run command : git pull 
it get data from git cloud repositry now rn these commads :

git status
git init
git add .
git commit -m "gh-pages setup "
git push origin master.


" Now go to worklfow to setup automation CI/CD"
just check your version of node on cmd by typing : 
node -v
and hit enter





Now go to this link https://github.com/settings/tokens

and click on genrate New Token that are called personal tocken which are nessary :
in name field type name of your token : deploy_access

and check the 4 boxes inside select scopes :

repo: status
repo_deployment
public_repo
repo_invite



just select those above and click on genrate tocken on bottom of that form.

and now you will see the string with mixed numbers and characters

looks like this : 5f2b6b********************************
copy that :

now go to your repositry back and click on setting and go to secrets
and hit new tocken a form will appear with two fieds name and value :
name of your secret  : 
i am using the name : ACTIONS_DEPLOY_ACCESS_TOKEN
paste the personal access token that we have genrated above in value filed : 5f2b6b********************************

hit add secret

----->
Now go to action and see your workflow click on yml file and click on penicl to edit 

DO not Copy this just type this avoid syntax errors:
Note:
add your usename of github 
add your email of github 
and other remain same if you ahve given the secret a differnt name then replae secrets.ACTIONS_DEPLOY_ACCESS_TOKEN this with secrets.Your_Name_of_Secret 
and commit the changes.
----->

# For more information see: https://help.github.com/actions/language-and-framework-guides/using-nodejs-with-github-actions

name: Node.js CI

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
    - name: Deploy
      run: |
        git config --global user.name 'ikishorkumar'
        git config --global user.email 'ikishorkumarofficial@gmail.com'
        git remote set-url origin https://${github_token}@github.com/${repository}
        npm run deploy
      env:
        user_name: 'github-actions[bot]'
        user_email: 'github-actions[bot]@users.noreply.github.com'
        github_token: ${{ secrets.ACTIONS_DEPLOY_ACCESS_TOKEN }}
        repository: ${{ github.repository }}




hit commit changes and commit it . and go actions and see your workflow working  correctly 
for this your repositry must be public  for priviate repositry github action to github pages : 
you might visit this one : 
https://github.com/JamesIves/github-pages-deploy-action
comunity help is there.




