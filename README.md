# Aboli_Assignment


# Q.1) Find the count of log statements in the attached(as access.log.zip) file “access.log” with successful response (status code 200).
# ANS:- 
For Unix-based Systems (Linux/macOS):
> Unzip the file:-
   unzip access.log.zip
> Count the number of lines with status code 200:-
   grep ' 200 ' access.log | wc -l

# Q.2) Write a command to find the files which contain words DEBUG, ERROR, and INFO in any directory of the filesystem.
# ANS:-
> To find files that contain the words DEBUG, ERROR, and INFO in any directory of the filesystem, I will use the grep command.
For Example:-
grep -rE 'DEBUG|ERROR|INFO'
> If you want to search a specific directory or set of directories, we can use '/' with the path to the directory you want to search.
For example:-
 grep -rE 'DEBUG|ERROR|INFO' /var/log

# Q.3) What would be the sed command to convert the string input "Ab1Cd2Ef3Gh4Ij5….." to "a-bc-de-fg-hi-j…."?
# ANS:-
Converts uppercase letters to lowercase.
Adds a dash after every second character.

Here's a sed command that accomplishes both:
echo "Ab1Cd2Ef3Gh4Ij5" | sed -E 's/([A-Z])/\L\1/g; s/([a-z0-9])([a-z0-9])/\1-\2/g'

# Q.4) 4. Write a script/program to return true if the opening and closing braces are complete, otherwise false.
e.g:
a. Input string:
List { information {{about the FILEs (the current directory by default). Sort entries alphabetically if} none of -cftuvSUX }nor --sort } is specified.
Output: True b. Input string:
Performs { the specified action on the files. { Valid actions are view, cat (uses only "copious output" rules { and sends output to STDOUT) , compose, com‐posetyped, edit and print. If no action is specified, the action will be determined by how the program was called.}
Output: False

# ANS:-
def are_braces_balanced(s):
    stack = []
    for char in s:
        if char == '{':
            stack.append(char)
        elif char == '}':
            if not stack or stack[-1] != '{':
                return False
            stack.pop()
    return not stack

for s in test_strings:
    print(f"Input string:\n{s}\nOutput: {are_braces_balanced(s)}\n")

 # Q.5) Write steps to create and publish a docker image to the docker repository. e.g., Run tomcat image with a customized landing page, and should be accessible at: http://localhost:8080/
 # ANS:- 
 Step-1) Prepare Custom Content
            Create index.html

Step-2)  Create Dockerfile
            FROM tomcat:latest
            COPY index.html /usr/local/tomcat/webapps/ROOT/
            EXPOSE 8080

Step-3)  Build the Docker Image
           docker build -t tomcat

Step-4)  Run the Docker Container
           docker run -d -p 8080:8080 tomcat

Step-5)  Verify
           Run tomcat image with a customized landing page, and should be accessible at :- http://localhost:8080/

Step-6)  Publish the Image

          docker login
          docker tag tomcat aboli21/tomcat
          docker push aboli21/tomcat

consider:- My Dockerhub Username :- aboli21

This setup creates a Docker image with a customized Tomcat server and publishes it to Docker Hub.

# Q.5) Bonus Question (Non Mandatory) 6. Given the following snippet of nginx server configuration: server {
listen 80 default_server; root /var/www/html;
server_name *.senpiper.com senpiper.com;
} Write a location block for requests “/api” that will include the proxied server: “http://localhost:8000/welcome/home”.

# ANS:- 
server {
    listen 80 default_server;
    root /var/www/html;
    server_name *.senpiper.com senpiper.com;

    location /api {
        proxy_pass http://localhost:8000/welcome/home;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

This configuration will route all requests starting with /api to the specified backend server at http://localhost:8000/welcome/home.



