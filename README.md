# React Native perspective image cropper 📐🖼

This library allows you to perform custom image crop and perspective correction.

![Demo image](https://s3-eu-west-1.amazonaws.com/michaelvilleneuve/demo-crop.gif)

This is a fork from this [repository](https://github.com/Michaelvilleneuve/react-native-perspective-image-cropper) and is designed to work with this [document detection library](https://github.com/cozy/react-native-document-scanner).



## Installation 🚀🚀

`$ yarn add react-native-perspective-image-cropper`


This library uses react-native-svg, you must install it too. See https://github.com/react-native-community/react-native-svg for more infos.

### Android Only

If you do not already have openCV installed in your project, add this line to your `settings.gradle`

```
include ':openCVLibrary310'
project(':openCVLibrary310').projectDir = new File(rootProject.projectDir,'../node_modules/react-native-perspective-image-cropper/android/openCVLibrary310')
```

## Crop image

- First get component ref

```javascript
<CustomCrop ref={ref => (this.customCrop = ref)} />
```

- Then call :

```javascript
this.customCrop.crop();
```

## Props

| Props                  | Type               | Required | Description                                                                             |
| ---------------------- | ------------------ | -------- | --------------------------------------------------------------------------------------- |
| `updateImage`          | `Func`             | Yes      | Returns the cropped image and the coordinates of the cropped image in the initial photo |
| `rectangleCoordinates` | `Object` see usage | No       | Object to predefine an area to crop (an already detected image for example)             |
| `initialImage`         | `String`           | Yes      | Base64 encoded image you want to be cropped                                             |
| `height`               | `Number`           | Yes      | Height of the image (will probably disappear in the future                              |
| `width`                | `Number`           | Yes      | Width of the image (will probably disappear in the future                               |
| `overlayColor`         | `String`           | No       | Color of the cropping area overlay                                                      |
| `overlayStrokeColor`   | `String`           | No       | Color of the cropping area stroke                                                       |
| `overlayStrokeWidth`   | `Number`           | No       | Width of the cropping area stroke                                                       |
| `handlerColor`         | `String`           | No       | Color of the handlers                                                                   |
| `enablePanStrict`      | `Bool`             | No       | Enable pan on X axis, and Y axis                                                        |

## Usage

```javascript
import CustomCrop from "react-native-perspective-image-cropper";

class CropView extends Component {
  componentWillMount() {
    Image.getSize(image, (width, height) => {
      this.setState({
        imageWidth: width,
        imageHeight: height,
        initialImage: image,
        rectangleCoordinates: {
          topLeft: { x: 10, y: 10 },
          topRight: { x: 10, y: 10 },
          bottomRight: { x: 10, y: 10 },
          bottomLeft: { x: 10, y: 10 }
        }
      });
    });
  }

  updateImage(image, newCoordinates) {
    this.setState({
      image,
      rectangleCoordinates: newCoordinates
    });
  }

  crop() {
    this.customCrop.crop();
  }

  render() {
    return (
      <View>
        <CustomCrop
          updateImage={this.updateImage.bind(this)}
          rectangleCoordinates={this.state.rectangleCoordinates}
          initialImage={this.state.initialImage}
          height={this.state.imageHeight}
          width={this.state.imageWidth}
          ref={ref => (this.customCrop = ref)}
          overlayColor="rgba(18,190,210, 1)"
          overlayStrokeColor="rgba(20,190,210, 1)"
          handlerColor="rgba(20,150,160, 1)"
          enablePanStrict={false}
        />
        <TouchableOpacity onPress={this.crop.bind(this)}>
          <Text>CROP IMAGE</Text>
        </TouchableOpacity>
      </View>
    );
  }
}
```

## Community

### What's Cozy?

<div align="center">
  <a href="https://cozy.io">
    <img src="https://cdn.rawgit.com/cozy/cozy-site/master/src/images/cozy-logo-name-horizontal-blue.svg" alt="cozy" height="48" />
  </a>
 </div>
 </br>

[Cozy] is a platform that brings all your web services in the same private space.  With it, your webapps and your devices can share data easily, providing you with a new experience. You can install Cozy on your own hardware where no one's tracking you.


### Get in touch

You can reach the Cozy Community by:

- Chatting with us on IRC [#cozycloud on Libera.Chat][libera]
- Posting on our [Forum][forum]
- Posting issues on the [Github repos][github]
- Say Hi! on [Twitter][twitter]


## License

This library is developed by cozy and distributed under the [AGPL v3 license][agpl-3.0].



[cozy]: https://cozy.io "Cozy Cloud"
[setup]: https://dev.cozy.io/#set-up-the-development-environment "Cozy dev docs: Set up the Development Environment"
[yarn]: https://yarnpkg.com/
[yarn-install]: https://yarnpkg.com/en/docs/install
[cozy-ui]: https://github.com/cozy/cozy-ui
[cozy-client-js]: https://github.com/cozy/cozy-client-js/
[cozy-stack-docker]: https://github.com/cozy/cozy-stack/blob/master/docs/client-app-dev.md#with-docker
[doctypes]: https://cozy.github.io/cozy-doctypes/
[bill-doctype]: https://github.com/cozy/cozy-konnector-libs/blob/master/models/bill.js
[konnector-doctype]: https://github.com/cozy/cozy-konnector-libs/blob/master/models/base_model.js
[konnectors]: https://github.com/cozy/cozy-konnector-libs
[agpl-3.0]: https://www.gnu.org/licenses/agpl-3.0.html
[contribute]: CONTRIBUTING.md
[tx]: https://www.transifex.com/cozy/
[tx-signin]: https://www.transifex.com/signin/
[tx-app]: https://www.transifex.com/cozy/<SLUG_TX>/dashboard/
[tx-client]: http://docs.transifex.com/client/
[libera]: https://web.libera.chat/#cozycloud
[forum]: https://forum.cozy.io/
[github]: https://github.com/cozy/
[twitter]: https://twitter.com/cozycloud
[nvm]: https://github.com/creationix/nvm
[ndenv]: https://github.com/riywo/ndenv
[jest]: https://facebook.github.io/jest/
