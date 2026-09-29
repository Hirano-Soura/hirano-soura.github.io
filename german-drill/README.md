# german-drill(ドイツ語 基礎暗記ドリル)

学習ポータル(hirano-soura.github.io)の「ドイツ語」カードから開くドリルです。
いまはハブのリポジトリの中に置いていますが、**将来は単独リポジトリ `german-drill` へ移す前提**で作っています。

## このフォルダの約束

移行を「フォルダを切り出すだけ」で済ませるため、次を守ります。

1. **このフォルダの外を参照しない。** パスはすべて相対で書き、`../` や `/german-drill/` のような絶対パスを使わない
2. **ハブとの接点は `status.js` だけ。** ハブは `webBase + status.js` を読み、`window.__portalStatus({...})` を受け取る。
   `status.js` はこのフォルダの直下に置き、`"id": "german"` を変えない
3. **フォルダ名は移行先のリポジトリ名と同じ `german-drill` にする。** GitHub Pages の URL
   `https://hirano-soura.github.io/german-drill/` が移行の前後で変わらない
4. **学習記録の localStorage キー(`de-kiso-drill-v1`)を変えない。** オリジン(`hirano-soura.github.io`)も移行の前後で同じなので、
   端末に残った記録はそのまま引き継がれる

約束 1 の確認(何も出なければよい):

```sh
grep -rnE '\.\./|/german-drill/' german-drill/ --exclude=README.md
```

## 中身

| ファイル | 役割 |
| --- | --- |
| `index.html` | ドリル本体。出題データも内蔵した 1 ファイル完結 |
| `status.js` | ハブのカードに出す状態 |
| `manifest.webmanifest` / `icon-*.png` | ホーム画面に追加したときの名前とアイコン |

## 単独リポジトリへの移行手順

ハブのリポジトリのルートで実行します。

1. フォルダの履歴だけを切り出す

   ```sh
   git subtree split --prefix=german-drill -b german-drill-export
   ```

2. GitHub で空のリポジトリ `german-drill` を作り、切り出したブランチを `main` として push する

   ```sh
   git push https://github.com/Hirano-Soura/german-drill.git german-drill-export:main
   ```

3. `german-drill` の Settings → Pages で `main` / `(root)` を公開元にする
4. ハブ側を更新する(同じコミットで行う)
   - `git rm -r german-drill`
   - `portals.js` の `german` の `repo` を `"german-drill"` に、`localBase` を手元の clone の位置(ハブからの相対)に変える。
     `webBase` は `/german-drill/` のまま変えない
5. `https://hirano-soura.github.io/` を開き、ドイツ語カードの状態表示とリンクが生きていることを確かめる

ハブのフォルダと単独リポジトリの Pages が同じパスで並んだ状態は、手順 3 と 4 の間だけにとどめます。
