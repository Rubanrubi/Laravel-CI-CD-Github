# Zero Downtime Laravel Deployments with Github Actions

   Step : 1  Folder Setup

               * First create .github/workflows directory in your project root directory,
               then store the deploy.yml in to that directory.

               * Inside the file first key => name which is displayed on github Actions on left shows Workflows inside
                 the name shown so we need to change that name means change that name key value

                       Eg : name: CI-CD

               * Then when the CI/CD Triggers? We need to specify on which branch getting pushed, 
                 so we need to specified like below:
                      
                       Eg : on:
                              push:
                                branches: [ development ]
                  
                * Next step will be inside jobs->deploy we mention the name key this is for once our CI/CD runs 
                    the jobs which are run in github workflows screen that name shows like a tag for the respective job
 
                * Inside that you need to mention the php versions 
                  installation process like composer install,php install and their extensions too.
                       
   
   Step : 2  Package Installation

                * Install the deployer package via composer,which is used for laravel automatically 
                  pipelined with github workflows to install that package run the command given below:
                     
                            composer require deployer/deployer deployer/recipes 

                 * Once you've got it installed, run ./vendor/bin/dep init and follow the prompts, 
                   selecting Laravel as your framework. 
                   A deploy.php config file will be generated and placed in the root of your project.

                 * In that deploy.php file we set the applicatio name by;

                            set('application', 'dep-demo');

                 * Then you don't want to take the things to production server means need to mention
                   in this method.

                        add('rsync', [
                            'exclude' => [
                                '.git',
                                '/.env',
                                '/storage/',
                                '/vendor/',
                                '/node_modules/',
                                '.github',
                                'deploy.php',
                            ],
                        ]);

                 * Then Must Configure this with server credentials
                         
                           // Hosts
                              host('your-IP') // Name of the server
                              ->hostname('your-IP') // Hostname or IP address
                              ->stage('production') // Deployment stage (production, staging, etc)
                              ->user('ubuntu or root')   // SSH User.
                              ->set('deploy_path', '/var/www/html');

                 * After that in task method need to add what are the commands need to run while running workflows,
                   like   config:cache,config:clear etc,
                   

                 * After running the above command ./vendor/bin/dep init it asks which frameworks,
                   and do you have configured github repo if github configured means hit enter and go
                   orelse need to give github repo url in it.

   Step : 3  Configuration

             * Then Go to Github your repository Settings->Secrets ,Here Need to add
               three key values which are;

                     1.SSH_KNOWN_HOST
                     2.DOT_ENV
                     3.SSH_PRIVATE_KEY

             * These three keys are configured in deploy.yml file,
               These three things must need to interat the ci/cd with that respective server
                so open your ssh terminal and run this command this will generates the SSH_KNOWN_HOST

                          ssh-keyscan rsa -t <server IP>

              * Then open your server .env file,then open your private key of that respective server

             *Paste all contents into that secret section in github by key values.

   Step : 4  Deployment Stage

              * Push the code to that branch open your workflows all the jobs getting runs,if any errors found during
                the run time need to fix then only that code deployed to server untill not,
                If the code looking fine means server gets updated source code.

              * While deploy the source code to server it deploys inside /var/www/html creates one directory
                called current inside that create the project

              * So After pointed to DNS go to etc/apache2/sites-available/confd file,change documentary root
                 to /var/www/html/current/public

              * That's It You Done!!!!!

              
             


                 
        
