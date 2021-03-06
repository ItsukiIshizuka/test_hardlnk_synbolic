# 【linux】ハードリンクとシンボリックリンクの違いと作り方
参照:<br>
https://penpen-dev.com/blog/symbolic-link-hardlink-tigai/<br>
https://www.infraeye.com/study/linuxz28.html<br>
https://ameblo.jp/julieta0089/entry-11267155850.html<br>
<br>

どちらもファイルの実体に対してリンクを生成するもの<br>
**ハードリンク** はリンク元と同じ`iノード`を持つリンクを作成する<br>
**シンボリックリンク** はリンク元と違う`iノード`を持つリンクを作成する
<br>

新規ファイルを作成時には必ず **１つ** のハードリンクが生成されている<br>
<br>

2つの違いは **リンク元ファイル削除時** の挙動にある。<br>
**ハードリンク** はリンク元ファイルを削除しても、ファイルの実体には **アクセスできる** 。
**シンボリックリンク** はリンク元ファイルを削除したら、ファイルの実体には **アクセスできない** 。

## リンク作成方法(linux)

```
// リンク元ファイルの確認
$ ls -al

30986465 drwxr-xr-x   7 *** ***   224  7  5 10:53 .
15799272 drwx------@ 19 *** ***   608  7  5 10:16 ..
30988415 -rw-r--r--   3 *** ***     6  7  5 10:41 test_origin.txt

// ハードリンク作成・ファイル確認
$ ln test_origin.txt lnk_h.ln
$ ls -ail

30986465 drwxr-xr-x   7 *** ***   224  7  5 10:53 .
15799272 drwx------@ 19 *** ***   608  7  5 10:16 ..
30988415 -rw-r--r--   3 *** ***     6  7  5 10:41 test_origin.txt
30988415 -rw-r--r--   3 *** ***     6  7  5 10:41 lnk_h.ln

// シンボリックリンク作成・ファイル確認
$ ln -s test_origin.txt lnk_s.ln
$ ls -ail

30986465 drwxr-xr-x   7 *** ***   224  7  5 10:53 .
15799272 drwx------@ 19 *** ***   608  7  5 10:16 ..
30988415 -rw-r--r--   3 *** ***     6  7  5 10:41 test_origin.txt
30988415 -rw-r--r--   3 *** ***     6  7  5 10:41 lnk_h.ln
30994578 lrwxr-xr-x   1 *** ***     9  7  5 10:47 lnk_s.ln -> test_origin.txt
```
