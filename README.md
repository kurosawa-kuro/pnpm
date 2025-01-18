# pnpm プロジェクト作成ガイド

## 環境構築
### WSLでのインストール
```bash
# Node.js/npmの削除
sudo apt remove nodejs npm
sudo apt autoremove

# fnmを使用したNode.jsのインストール
curl -fsSL https://fnm.vercel.app/install | bash
source ~/.bashrc
fnm install --lts

# pnpmのインストール
curl -fsSL https://get.pnpm.io/install.sh | sh -
source ~/.bashrc
```

### Amazon Linux 2023でのインストール
```bash
# Node.js/npmの削除
sudo dnf remove nodejs npm
sudo dnf clean all

# Node.jsのインストール
curl -fsSL https://rpm.nodesource.com/setup_lts.x | sudo bash -
sudo dnf install -y nodejs

# pnpmのインストール
curl -fsSL https://get.pnpm.io/install.sh | sh -
source ~/.bashrc
```

## Next.jsプロジェクトの作成
1. プロジェクトの初期化
```bash
pnpm create next-app my-nextjs-project
```

2. 推奨設定
```bash
TypeScript: Yes
ESLint: Yes
Tailwind CSS: Yes
src/ directory: Yes
App Router: Yes
import alias: No
```

3. 開発サーバーの起動
```bash
cd my-nextjs-project
pnpm dev
```

### パッケージ管理
```bash
# 通常パッケージの追加
pnpm add パッケージ名

# 開発用パッケージの追加
pnpm add -D パッケージ名
```

## CDKプロジェクトの作成
1. プロジェクト初期化
```bash
mkdir my-cdk-project
cd my-cdk-project
pnpm init
```

2. 依存パッケージのインストール
```bash
# CDK関連
pnpm add -D aws-cdk aws-cdk-lib constructs

# TypeScript関連
pnpm add -D typescript @types/node ts-node
```

3. プロジェクト構造の作成
```bash
mkdir bin lib
```

### 設定ファイル
1. tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["es2020"],
    "declaration": true,
    "strict": true,
    "typeRoots": ["./node_modules/@types"]
    // その他の設定は必要に応じて追加
  },
  "exclude": ["node_modules", "cdk.out"]
}
```

2. package.json (scripts)
```json
{
  "scripts": {
    "build": "tsc",
    "watch": "tsc -w",
    "cdk": "cdk",
    "deploy": "cdk deploy",
    "destroy": "cdk destroy"
  }
}
```

### 基本ファイル構造
```
my-cdk-project/
├── bin/
│   └── my-cdk-app.ts    # エントリーポイント
├── lib/
│   └── my-stack.ts      # スタック定義
├── package.json
└── tsconfig.json
```

### デプロイ
```bash
pnpm run deploy
```

## 注意事項
- プロジェクトに応じて.gitignoreの設定
- cdk.jsonの必要性を確認
- 必要なパッケージは適宜追加
