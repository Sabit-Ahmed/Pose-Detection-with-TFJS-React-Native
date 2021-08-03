# Pose-Detection

## Steps
1. `npx create-react-native-app rn8app`
2. `yarn add react-native-unimodules expo-gl-cpp expo-gl expo-camera jpeg-js @react-native-community/async-storage react-native-fs expo-permissions expo-file-system expo-image-picker @tensorflow/tfjs @tensorflow/tfjs-react-native`
3. `react-native link react-native-fs`
4. Add following lines in android/build.gradle (for expo-camera):
    allprojects {
        repositories {

            // * Your other repositories here *

            // * Add a new maven block after other repositories / blocks *
            maven {
                // expo-camera bundles a custom com.google.android:cameraview
                url "$rootDir/../node_modules/expo-camera/android/maven"
            }
        }
    }
    
5. add these lines in in AndroidManifest.xml for image-cropping functionality:
    <activity
        android:name="com.theartofdev.edmodo.cropper.CropImageActivity"
        android:theme="@style/Base.Theme.AppCompat">
    </activity>



#### For this project
If you want to use TypeScript in your project:

i.  Add TypeScript and the types for React Native and Jest to your project.
    `yarn add -D typescript @types/jest @types/react @types/react-native @types/react-test-renderer`
    
ii.  Add a TypeScript config file. Create a tsconfig.json in the root of your project:
    
    {
        "compilerOptions": {
            "allowJs": true,
            "allowSyntheticDefaultImports": true,
            "esModuleInterop": true,
            "isolatedModules": true,
            "jsx": "react",
            "lib": ["es6"],
            "moduleResolution": "node",
            "noEmit": true,
            "strict": true,
            "target": "esnext"
        },
        "exclude": [
            "node_modules",
            "babel.config.js",
            "metro.config.js",
            "jest.config.js"
        ]
    }
    
iii. Create a jest.config.js file to configure Jest to use TypeScript:
    
    module.exports = {
        preset: 'react-native',
        moduleFileExtensions: ['ts', 'tsx', 'js', 'jsx', 'json', 'node']
    };
    
iv. Rename a JavaScript file to be *.tsx

v.  Run `yarn tsc` to type-check your new TypeScript files.


7.  Add ".png" in metro.config.js in the resolver:
    assetExts: ['bin', 'txt', 'jpg', 'png']

(Replace the metro.config.js with the following codes):
    
    const blacklist = require('metro-config/src/defaults/blacklist');
    module.exports = {
        transformer: {
            getTransformOptions: async () => ({
                transform: {
                    experimentalImportSupport: false,
                    inlineRequires: false,
                },
            }),
        },
        resolver: {
            assetExts: ['bin', 'txt', 'jpg', 'png'],
            sourceExts: ['js', 'json', 'ts', 'tsx', 'jsx'],
            blacklistRE: blacklist([/platform_node/])
        },
    };

8.  `yarn add @tensorflow-models/blazeface @tensorflow-models/mobilenet @tensorflow-models/posenet expo-image-manipulator jasmine-core react-native-svg rn-fetch-blob`

9. Run model's local server with `http-server -c1 --cors .`


#### Important Notes
Expo-camera does not have support for emulator, so test this project with real devices with released apk by `cd android && ./gradlew clean && ./gradlew assembleRelease && cd ..`
* Command for release build apk: `cd android && ./gradlew clean && ./gradlew assembleRelease && cd ..`
* After release build, next time use `cd android && ./gradlew clean` to clean the files created when bundling. 
* And run `npx react-native run-android` for debug or `cd android && ./gradlew clean && ./gradlew assembleRelease && cd ..` for release.
