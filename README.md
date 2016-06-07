# gradleHelper
scripts to include in build.gradle files

To deploy and use a custom AAR library as a dependency in your android project do the following:
-	In your main project build.gradle file add the lines :
<P>
```
allprojects {
    repositories {
        jcenter()
        maven {
            url "https://raw.github.com/synergian/wagon-git/releases"
        }
        maven {
            url REPOSITORY_RAW_URL
            credentials {  //should place these properties in the private ${userHome}.gradel/gradle.properties file :
                username = REPOSITORY_USERNAME
                password = REPOSITORY_PASSWORD
            }
        }
        mavenLocal()
    }
}

```
</P>
- In the project  gradle.properties fill the propertie value : for i.e :
```properties 
PUBLISH_RELEASE_DEST = git:releases://git@bitbucket.org:myLogin/myRepositoryLib.git
REPOSITORY_RAW_URL = https://api.bitbucket.org/1.0/repositories/myLogin/myRepositoryLib/raw/releases
```
 
Then in the build.gradle file of the module AAR  you want to upload simply add :
```
apply from: 'https://raw.githubusercontent.com/tcDeployTool/gradleHelper/master/android-release-aar.gradle'
```

And in the module's gradle.properties file fill the corresponding properties for i.e. :
```properties
PUBLISH_GROUP_ID = com.mylib
PUBLISH_ARTIFACT_ID = mylibrarymodule1
PUBLISH_VERSION = 1.0.0
```

