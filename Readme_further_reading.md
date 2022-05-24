## Serving  pages with your own Domain Name 

![](readme_img/domain.png)

### Domain Registration
#### Check if a domain name is available
- https://www.huaweicloud.com/product/domain.html
- https://wanwang.aliyun.com/domain/
- https://dnspod.cloud.tencent.com/


#### Sales
- https://cloud.tencent.com/act/domainsales
- https://activity.huaweicloud.com/discount_area_v5/index.html
- https://activity.huaweicloud.com/promotion/
- https://activity.huaweicloud.com/domain1.html
- https://wanwang.aliyun.com/domain/yumingheji
- https://cn.aliyun.com/activity

### Method 1: Web hosting service by Alibaba, Tencent and Huawei
- https://help.aliyun.com/document_detail/31872.html
- https://cloud.tencent.com/product/wh
- https://support.huaweicloud.com/ugobs-obs/obs_41_0036.html

How:
- http:// pageshu. xyz or top (buy from: https://cloud.tencent.com/act/domainsales)


###  Method 2: Pointing Domain to Cloud VM's Public IP Address
 
![](readme_img/point.png)

- http:// pageshu. xyz or top (buy from: https://activity.huaweicloud.com/domain1.html)


## Cloud VM Pages with HTTPS
![](readme_img/https.png)
If you want to have HTTPS, you should proceed with 网站备案 first.
- https://cloud.tencent.com/document/product/243

You should also apply for an SSL certificate.
- https://cloud.tencent.com/document/product/400/7572

HTTPS uses port 443.


## WH Pages Automatic deployment with GitHub Webhook 

Github Webhook -> VM pull -> VM ```cloudbase ``` CLI update folder. https://cloud.tencent.com/document/product/876/47142



## Hugo Dockerization 
- https://dev.to/eduardort/hugo-and-nginx-multi-stage-build-dockerfile-3o63
- https://www.bravoslab.com/post/static-website-wirh-hugo.io-and-ngnix/
- https://github.com/jtreminio/hugoBasicExample


## Re-clone submodule
If for some reason your submodule doesn't work, here is how:
```shell script
git rm --cached themes/ananke
git rm .gitmodules             
rm -rf themes/ananke/.git 
rm -rf themes/ananke
touch .gitmodules
git submodule add --force git@github.com:theNewDynamic/gohugo-theme-ananke.git themes/ananke
git add .
git commit -m "re-clone submodule"
```

## Overleaf
If you want to generate very beautiful CV pdf:
- https://www.overleaf.com/gallery/tagged/cv



##  [optional] Let's Dockerize this repository  

### Remove git submodules
![](readme_img/submodule.png)

```shell script
# Ref: https://stackoverflow.com/questions/1759587/how-to-un-submodule-a-git-submodule
git rm --cached submodule_path 
git rm .gitmodules             
rm -rf submodule_path/.git     
git add submodule_path         
git commit -m "remove submodule"
```

### Gitee.com, in addition to GitHub
![](readme_img/gitee.png)

### Dockerfile multistage build
![](readme_img/build.png)

- https://docs.docker.com/develop/develop-images/multistage-build/

```shell script
#------------- STAGE 1 -------------#
FROM alpine/git as download
WORKDIR /site
RUN git clone https://gitee.com/lundechen/static_website_with_go_hugo

#------------- STAGE 2 -------------#
# Ref: https://github.com/peaceiris/hugo-extended-docker
FROM peaceiris/hugo:v0.86.0-mod as build
COPY --from=download /site/static_website_with_go_hugo /site
WORKDIR /site
RUN hugo --minify

#------------- STAGE 3 -------------#
FROM nginx:lastest
WORKDIR /usr/share/nginx/html/
# The "public" folder generated by Hugo in the previous stage
# is copied into the public fold of nginx
COPY --from=build /site/public /usr/share/nginx/html
```


## [optional] Ship the Dockerfile to DockerHub   

![](readme_img/dockerhub.png)

So that one can run this project with one simple Docker commandline.
