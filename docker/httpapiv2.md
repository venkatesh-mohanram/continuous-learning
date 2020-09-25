# Using the remote REST API to perform all things
Most of the time when it comes to docker, we play with using the CLI with 'docker' command. If we want to pull an image, tag an image, push an image we do all that with CLI only. 
However apart from CLI, the docker repository supports varieties of REST API to do plenty of things and here I am planning to cover few thins like below
1. [Manifest resource](#manifest)  

<a name="manifest"></a>

## Manifest resource
The manifest rest resource can be used in a way how we want, for eg: if we want to know whether the image exist with a given tag then we can use the GET method of it

``` python
def checkAlreadyPresent(imageName, tag, bearerToken):
    auth_header = {'Authorization': ''}
    auth_header['Authorization'] = 'Bearer ' + bearerToken
    res = requests.get(
            url="https://docker.io/v2/" + imageName + "/manifests/" + tag,
            headers=auth_header)
    return res.status_code
``` 