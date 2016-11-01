# take screenshot and save to local file system
```
browser.takeScreenshot().then((base64png) => {
    let stream = fs.createWriteStream(testName + '.png');
    stream.write(new Buffer(base64png, 'base64'));
    stream.end();
});
```
## jasmine
### **testName** could be taken via
* [jasmine](http://jasmine.github.io/)  [custom reporter](http://jasmine.github.io/2.4/custom_reporter.html) functionality
* `jasmine.getEnv().currentSpec`
* other options

## **cucumber**
### testName could be taken via
* scenario output of 'after' hook
* other options

# take screenshot and attach to cucumber output .json file (for CI Jenkins [Cucumber plugin](https://github.com/damianszczepanik/cucumber-reporting) as example)
```
import {browser} from 'protractor';

export = function () {

    this.After((scenario, done) => {
        if (scenario.isFailed()) {
            return browser.takeScreenshot().then(base64png => {
                let decodedImage = new Buffer(base64png, 'base64').toString('binary');
                scenario.attach(decodedImage, 'image/png');
            }, (err) => {
                done(err);
            });
        } else {
            done();
        }
    });

}
```