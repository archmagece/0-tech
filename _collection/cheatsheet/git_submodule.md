# git submodule

서브모듈은 해당 git 리포지터리의 특정 스냅샷을 사용하는 경우에만 사용

## submodule을 사용하는 경우와 아닌 경우 사례

테스트를 위해서 특정 리포지터리를 가져와야하는경우??
  git clone 스크립트 활용



```sh
git submodule add --name api-stream git@bitbucket.org:cosmicbc/mex-api-stream.git projects/api-stream
git submodule add --name api-trade git@bitbucket.org:cosmicbc/mex-api-trade.git projects/api-trade
git submodule add --name api-user git@bitbucket.org:cosmicbc/mex-api-user.git projects/api-user

git submodule add --name engine-prefilter git@bitbucket.org:cosmicbc/mex-engine-prefilter.git projects/api-stream
git submodule add --name engine-matching git@bitbucket.org:cosmicbc/mex-engine-matching.git projects/engine-matching
git submodule add --name engine-postfilter git@bitbucket.org:cosmicbc/mex-engine-postfilter.git projects/engine-postfilter

git submodule add --name index git@bitbucket.org:cosmicbc/mex-index.git projects/index
git submodule add --name wallet git@bitbucket.org:cosmicbc/mex-wallet.git projects/wallet
```

### change branch

git submodule sync
git submodule update --init --recursive
