# DockerComposeWalkthrough1
DockerComposeWalkthrough1

Download and install docker engine and compose before taking this walkthrough.

Assuming Docker Engine and Compose is installed.
Step 1: Setup Define the application dependencies. 
    1. Create a directory for the project: 
    2. $ mkdir composetest 
    3. $ cd composetest 
    4. Create a file called app.py in your project directory 
    
    In this example, redis is the hostname of the redis container on the application’s network. We use the default port for Redis, 6379.
  1. Create another file called requirements.txt in your project directory 
Step 2: Create a Dockerfile In this step, you write a Dockerfile that builds a Docker image. 
        The image contains all the dependencies the Python application requires, including Python itself.
        In your project directory, create a file named Dockerfile. 
        This tells Docker to:  Build an image starting with the Python 3.4 image.  
        Add the current directory . into the path /code in the image.  
        Set the working directory to /code.  
        Install the Python dependencies.  
        Set the default command for the container to python app.py. 
Step 3: Define services in a Compose file Create a file called docker-compose.yml in your project directory.
        This Compose file defines two services, web and redis. 
        The web service: Uses an image that’s built from the Dockerfile in the current directory. 
        Forwards the exposed port 5000 on the container to port 5000 on the host machine. 
        We use the default port for the Flask web server, 5000. 
        The redis service uses a public Redis image pulled from the Docker Hub registry. 
Step 4: Build and run your app with Compose 
        1. From your project directory, start up your application by running docker-compose up. 
        2. $ docker-compose up  
        This shows following output and blocks this window.....
        3. Creating network "composetest_default" with the default driver 
        4. Creating composetest_web_1 ... 
        5. Creating composetest_redis_1 ... 
        6. Creating composetest_web_1 
        7. Creating composetest_redis_1 ... done 
        8. Attaching to composetest_web_1, composetest_redis_1 
        9. web_1 | * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit) 
        10. redis_1 | 1:C 17 Aug 22:11:10.480 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo 
        11. redis_1 | 1:C 17 Aug 22:11:10.480 # Redis version=4.0.1, bits=64, commit=00000000, modified=0, pid=1, just started 
        12. redis_1 | 1:C 17 Aug 22:11:10.480 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
        13. web_1 | * Restarting with stat 
        14. redis_1 | 1:M 17 Aug 22:11:10.483 * Running mode=standalone, port=6379. 
        15. redis_1 | 1:M 17 Aug 22:11:10.483 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128. 
        16. web_1 | * Debugger is active! 17. redis_1 | 1:M 17 Aug 22:11:10.483 # Server initialized 
        18. redis_1 | 1:M 17 Aug 22:11:10.483 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled. 
        19. web_1 | * Debugger PIN: 330-787-903 redis_1 | 1:M 17 Aug 22:11:10.483 * Ready 
        
        1. Compose pulls a Redis image, builds an image for your code, and starts the services you defined. 
           In this case, the code is statically copied into the image at build time. 
        2. Enter http://0.0.0.0:5000/ in a browser to see the application running. 
           If you’re using Docker natively on Linux, Docker for Mac, or Docker for Windows, then the web app should now be listening on port 5000 on your Docker daemon host. 
          Point your web browser to http://localhost:5000to find the Hello World message. 
          
          If this doesn’t resolve, you can also tryhttp://0.0.0.0:5000.
          You should see a message in your browser saying: Hello World! I have been seen 1 times. 
          Refresh the page. The number should increment. Hello World! I have been seen 2 times. 
         3. Switch to another terminal window, and type docker image ls to list local images. 
           Listing images at this point should return redis and web. 
           
