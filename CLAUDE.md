# CLAUDE.md

このファイルは、このリポジトリで Claude Code (claude.ai/code) が作業する際のガイダンスです。

## プロジェクト概要

task-board プロジェクト。React 製のシンプルなタスクボードアプリ(タスクの追加・完了切り替え・削除、localStorage への永続化)。

## 技術スタック

- **React 19** + **Vite** (`@vitejs/plugin-react`)
- 言語: JavaScript (JSX)。TypeScript は未導入。
- Lint: **oxlint** (`npm run lint`)
- 状態管理: React 標準の `useState` / `useEffect` のみ。外部の状態管理ライブラリは使用しない。
- データ永続化: ブラウザの `localStorage`(バックエンド API・DB は無し)
- デプロイ: **GitHub Actions** (`.github/workflows/deploy.yml`) で `main` への push をトリガーに自動ビルド・**GitHub Pages** へデプロイ

## デプロイ先

- https://okmorz.github.io/task-board/
- `main` ブランチに push すると GitHub Actions が自動でビルドし、上記 URL に反映される。
- `vite.config.js` の `base: '/task-board/'` はリポジトリ名と一致させること(リポジトリ名を変更する場合はここも合わせて変更する)。

## コンポーネントの命名規約

- コンポーネントは **PascalCase** で命名し、ファイル名もコンポーネント名と一致させる(例: `App.jsx` → `function App()`)。
- 1 ファイル 1 コンポーネントを基本とする。
- コンポーネント用の CSS は同名の `.css` ファイルに分け、コンポーネントファイルと同じディレクトリに置く(例: `App.jsx` + `App.css`)。
- 関数・変数・イベントハンドラは **camelCase**(例: `addTask`, `toggleTask`, `deleteTask`)。イベントハンドラは動詞から始める名前にする。
- `src/` 直下にコンポーネントを置き、コンポーネント数が増えたら `src/components/` などのサブディレクトリへ整理する。

## Git 運用ルール

- **コードを変更するたびに、必ず GitHub へ push すること。** 変更を作業ツリーに残したままにしない。
- コミットは小さく、目的が分かる単位で作成する。
- コミットメッセージは「なぜ変更したか」が分かるように簡潔に書く。
- push 前に `git status` / `git diff` で差分を確認し、意図しないファイル(認証情報や不要なビルド成果物など)が含まれていないかチェックする。
- force push (`--push --force` 等)や履歴を書き換える操作は行わない。必要な場合は必ず事前に確認を取る。
- リモートリポジトリ (origin) が未設定の場合は、push 前にユーザーに確認する。

## 開発コマンド

- `npm install` — 依存関係のインストール
- `npm run dev` — 開発サーバー起動
- `npm run build` — 本番ビルド(`dist/` に出力)
- `npm run lint` — oxlint による静的解析
- `npm run preview` — ビルド成果物のプレビュー
