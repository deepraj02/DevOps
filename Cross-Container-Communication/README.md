# Container Communication


## Container-Container Communication..
### Sol: Map the containers in a custom network
#### Steps:
- [x] Create a custom Network
``` bash
docker network create <network name>
```
- [x]  Running 1st container in the defined network (mongodb)
```bash
docker run -d --rm --name mongodb --network favs-app-network mongo
```
- [x] Running the second container (favs-app)
```bash
docker run -d --rm --name favs-cont -p 3000:3000 --network favs-app-network favs-app
```
- [x] Change the URL in to the container name 
```js
mongoose.connect(
    // mongodb is the container name
  'mongodb://mongodb:27017/swfavorites',
  { useNewUrlParser: true },
  (err) => {
    if (err) {
      console.log(err);
    } else {
      app.listen(3000);
    }
  }
);

```