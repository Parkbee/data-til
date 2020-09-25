# ParkBee Data Today-I-Learned

You can serve it locally by running:

```
docker run --rm --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" -it -p 4000:4000 --env JEKYLL_ENV=development jekyll/jekyll:3.8.6 jekyll serve
```
