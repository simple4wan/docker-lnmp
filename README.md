# alias

```bash
alias redis-cli='docker run --rm -it -u redis docker-lnmp_redis redis-cli'
alias mysql='docker run --rm -it -u mysql docker-lnmp_mysql mysql'
alias php='docker run --rm -it -v $(pwd):/Documents -u www-data docker-lnmp_php php'
alias composer='docker run --rm -it -v $(pwd):/Documents -u www-data docker-lnmp_php composer'
```

