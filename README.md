# Zero Downtime Laravel Deployments with Github Actions

   Step : 1  Folder Setup

               * First create .github/workflows directory in your project root directory,
               then store the deploy.yml in to that directory.

               * Inside the file first key => name which is displayed on github Actions on left shows Workflows inside
                 the name shown so we need to change that name means change that name key value

                       Eg : name: CI-CD

               * Then when the CI/CD Triggers? We need to specify on which branch getting pushed, so we need to specified like below:
                      
                       Eg : on:
                              push:
                                branches: [ development ]
                  
                * Next step will be inside jobs->deploy we mention the name key this is for once our CI/CD runs 
                    the jobs which are run in github workflows screen that name shows like a tag for the respective job
 
                * Inside that you need to mention the php versions 
                  installation process like composer install,php install and their extensions too.
                       
   
   Step : 2  Package Installation

                * Install the deployer package via composer,which is used for laravel automatically pipelined with github workflows
                  to install that package run the command given below:
                     
                            composer require deployer/deployer deployer/recipes 

                 * Once you've got it installed, run ./vendor/bin/dep init and follow the prompts, selecting Laravel as your framework. 
                   A deploy.php config file will be generated and placed in the root of your project.


                 
        
