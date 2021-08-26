# Terraform-spotify

Create a playlist on Spotify by writing it as a Terraform configuration.

1. You should have a spotify developer access.
2. Go to https://developer.spotify.com/dashboard/applications
3. Create a new app.
4. Go to edit setting and add a redirect URIs i.e http://localhost:27228/spotify_callback and click add , scroll down and save.
5. Get the client ID and Client secret for your application.
6. Now, export the callback url on your terminal as,
        
        export SPOTIFY_CLIENT_REDIRECT_URI=http://localhost:27228/spotify_callback

7. Create a new file name .env in the top root folder and add the following content with client key and client secret.
        
        SPOTIFY_CLIENT_ID=
        SPOTIFY_CLIENT_SECRET=

8. Now, run the docker container to create a authn proxy server to get the oauth token from spotify.

        docker run --rm -it -p 27228:27228 --env-file ./.env ghcr.io/conradludgate/spotify-auth-proxy

After you run above command you will get the api_key and auth_url. 

9. Now click on the auth-url, accept and verify your account and complete the authorization.
10. Now keep the container running and copy the api_key.
11. Rename this file "terraform.tfvars.example"
        
        mv terraform.tfvars.example terraform.tfvars

12. Paste your api_key in "terraform.tfvars"
13. Now, initialize the terraform.
        
        terraform init

14. Apply the terraform
        
        terraform apply

15. Now open your spotify account and listen the newly created playlist using terraform.