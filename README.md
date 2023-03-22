# alias

```bash
alias redis-cli='docker run --rm -it -u redis redis redis-cli'
alias mysql='docker run --rm -it -u mysql mariadb mysql'
alias php='docker run --rm -it -v $(pwd):/Documents -u www-data docker-lnmp-php7 php'
alias composer='docker run --rm -it -v $(pwd):/Documents -u www-data docker-lnmp-php7 composer'
```

