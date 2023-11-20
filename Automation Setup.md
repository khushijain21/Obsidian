```
git clone "[https://tpallavi@gerrit.ext.net.nokia.com/gerrit/a/CSF-FPM-TEST"](https://tpallavi@gerrit.ext.net.nokia.com/gerrit/a/CSF-FPM-TEST%22 "https://tpallavi@gerrit.ext.net.nokia.com/gerrit/a/csf-fpm-test%22") && (cd "CSF-FPM-TEST" && gitdir=$(git rev-parse --git-dir); curl -o ${gitdir}/hooks/commit-msg [https://gerrit.ext.net.nokia.com/gerrit/static/commit-msg](https://gerrit.ext.net.nokia.com/gerrit/static/commit-msg "https://gerrit.ext.net.nokia.com/gerrit/static/commit-msg") ; chmod +x ${gitdir}/hooks/commit-msg)
```


clone CFS-FPM-TEST
git checkout CSF-FPM-TEST-2.0

in requirements.txt - remove aws-nokia-login
pip3 install -r requirements.txt

export PYTHONPATH=$PWD/radish
and create 1 vanilla cluster

radish <feature file> -t --cucumber-json output/radish_test_result.json --write-ids --no-line-jump




![[Pasted image 20231115173039.png]]




