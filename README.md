# arbuh.github.io

## How to

### Covert slides to HTML

Using Marp CLI:

```bash
marp slides.md --theme-set custom-theme.css
```

Using Docker:

```bash
docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER="$(id -u):$(id -g)" -e LANG=$LANG marpteam/marp-cli gmgc.md
```
