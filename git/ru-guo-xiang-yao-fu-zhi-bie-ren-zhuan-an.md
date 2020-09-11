# 如果想要複製別人專案

進入專案後，把remote內的origin給替換成自己的，在push上去即可。

```bash
cd <projectName>
git remote -v
git remote remove origin
git remote add origin <git-project-git@git@...>
git push -u origin master
```

