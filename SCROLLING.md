# SCROLL INTO ELEMENT VIEW
```
import { browser, $} from 'protractor';
...
let someElement = $('.someClass');
browser.executeScript('arguments[0].scrollIntoView(true);', someElement.getWebElement());
...
```
some kind of reusable util method could possibly looks like:
```
import { browser} from 'protractor';

export class BrowserHelper {

  static scrollIntoView (el) {
    return browser.executeScript('arguments[0].scrollIntoView(true);', el.getWebElement());
  }

}
```
