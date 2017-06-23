# Sidekiq Web Google Sign In

Restrict access to your Sidekiq using Google Sign In.

## Installation

1. Visit [Google Developers Console](console.developers.google.com)

2. Create a project. Give it a name like "My Application Sidekiq Web".

3. Click on the "Library" section in the sidebar. Search for "Contacts API". Enable it. Now, search for "Google+ API" and enable that as well.

4. Click on the "Credentials" section in the sidebar and then click on the "OAuth consent screen" at the top. Fill the OAuth consent screen form and click Save.

5. Click on the "Create credentials" button and choose "OAuth client ID" in the menu that pops up. Select "Web application" as the Application Type. Enter a name like "My Application Sidekiq Web". Enter a URL like https://myapplication.com/sidekiq/auth/google_oauth2/callback in the "Authorized redirect URIs" field and click Create.

6. Copy the displayed client id and secret

7. Add the `sidekiq_web_google_sign_in` gem to your Gemfile

   ```ruby
   gem "sidekiq_web_google_sign_in"
   ```

   and run

   ```
   bundle install
   ```

8. Create the file `config/initializers/sidekiq_web_google_sign_in.rb` and copy paste the code below

   ```ruby
   SidekiqWebGoogleSignIn.use :google_sign_in_client_id => "my_client_id",
                              :google_sign_in_client_secret => "my_client_secret",
                              :employee_emails => Proc.new { |email| email.end_with?("@myapplication.com") }
   ```

   Replace `my_client_id` and `my_client_secret` with your actual client id and secret