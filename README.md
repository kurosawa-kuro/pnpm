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

cdk init app --language typescript

rm -rf node_modules
rm package-lock.json

pnpm install
```

```
{
  "scripts": {
    "build": "tsc",
    "watch": "tsc -w",
    "test": "jest",
    "cdk": "cdk"
  },
  "devDependencies": {
    "@types/jest": "^29.5.8",
    "@types/node": "20.9.1",
    "jest": "^29.7.0",
    "ts-jest": "^29.1.1",
    "aws-cdk": "2.114.1",
    "ts-node": "^10.9.1",
    "typescript": "~5.2.2"
  },
  "dependencies": {
    "aws-cdk-lib": "2.114.1",
    "constructs": "^10.0.0",
    "source-map-support": "^0.5.21"
  }
}
```

## 注意事項
- プロジェクトに応じて.gitignoreの設定
- cdk.jsonの必要性を確認
- 必要なパッケージは適宜追加
