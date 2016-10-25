Demo of `@Grab` support in Jenkins Pipeline global libraries. ([Official documentation](https://github.com/jenkinsci/workflow-cps-global-lib-plugin#using-third-party-libraries))

To use, go to system configuration and create a new global library.
Give it the name `grapedemo` and a default version `master`.
Using *Legacy SCM* and *Git*, set the remote URL to `https://github.com/jglick/grapedemo` and set the branch specifier to `${library.grapedemo.version}`.

Now you can use the library in a `Jenkinsfile`, for example:

```groovy
@Library('grapedemo') import grapedemo.Lib
def prime = 0
try {
    timeout(time: 10, unit: 'SECONDS') {
        for (int n = 2; true; n++) {
            if (Lib.isPrime(n)) {
                prime = n
            }
        }
    }
} finally {
    echo "got as far as $prime"
}
```
