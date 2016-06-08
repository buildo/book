# Step 0

Start by downloading [this zipfile](https://github.com/buildo/webseed/archive/tutorial-step0.zip) which includes all the boilerplate you need.

The boilerplate is not documented at the moment, so treat it as a black box. There is an [open issue](https://github.com/buildo/webseed/issues/18) about reducing the necessary boilerplate.

You should be able to do:

```sh
unzip webseed-tutorial-step0.zip
cd webseed-tutorial-step0/
cp config-development.json.example config.json
npm i
npm start
```

If everything works, your app should be running at http://localhost:9090/