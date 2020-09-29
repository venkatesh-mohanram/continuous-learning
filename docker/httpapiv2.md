# Using the remote REST API to perform all things
Most of the time when it comes to docker, we play with using the CLI with 'docker' command. If we want to pull an image, tag an image, push an image we do all that with CLI only. 
However apart from CLI, the docker repository supports varieties of REST API to do plenty of things and here I am planning to cover few thins like below
1. [Manifest resource](#manifest)
2. [Remote tagging](#remote_tagging)  

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

<a name="remote_tagging"></a>

## Remote tagging
If we want to tag a certain docker image with additional tags then we can use the manifests REST API to do that, below is the python example of doing the same

``` python
def addAssociatedTag(imageName, tag, associatedTag, bearerToken):
    header = {'Authorization': ''}
    header['Authorization'] = 'Bearer ' + bearerToken
    header['Accept'] = 'application/vnd.docker.distribution.manifest.v2+json'
    res = requests.get(
            url="https://docker.io/v2/" + imageName + "/manifests/" + tag,
            headers=header)
    print('Retrieved the metifests status is ' + str(res.status_code))   
    # Add the associated tag by passing the same manifests
    header['Accept'] = '*'
    res = requests.request(
            "PUT",
            url="https://docker.io/v2/" + imageName + "/manifests/" + associatedTag,
            headers=header,
            data=res.content)      
    response_status = res.status_code
    print('Adding associated tag for ' + imageName + ':' + tag + ' with ' + imageName + ':' + associatedTag + ' is = ' + str(response_status))
    return response_status
```