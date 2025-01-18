# pnpm

WSLとAmazon Linux 2023それぞれのpnpmインストール手順と、npmのアンインストール方法をご説明します。

**WSLでのpnpmインストール**
```bash
# curlのインストール（なければ）
sudo apt update
sudo apt install curl

# Node.jsをアンインストール（既存のnpmも削除される）
sudo apt remove nodejs npm
sudo apt autoremove

# fnmを使ってNode.jsをインストール
curl -fsSL https://fnm.vercel.app/install | bash
source ~/.bashrc
fnm install --lts

# pnpmのインストール
curl -fsSL https://get.pnpm.io/install.sh | sh -
source ~/.bashrc
```

**Amazon Linux 2023でのpnpmインストール**
```bash
# Node.jsをアンインストール（既存のnpmも削除される）
sudo dnf remove nodejs npm
sudo dnf clean all

# Node.jsリポジトリの追加とインストール
curl -fsSL https://rpm.nodesource.com/setup_lts.x | sudo bash -
sudo dnf install -y nodejs

# pnpmのインストール
curl -fsSL https://get.pnpm.io/install.sh | sh -
source ~/.bashrc
```

**npmの手動アンインストール（必要な場合）**
```bash
# npmのグローバルパッケージの確認
npm list -g --depth=0

# グローバルパッケージの削除
sudo npm uninstall -g パッケージ名

# npmの完全削除
sudo rm -rf /usr/local/bin/npm
sudo rm -rf /usr/local/lib/node_modules/npm
sudo rm -rf ~/.npm
```

インストール後の確認：
```bash
pnpm --version
node --version
```

注意点：
- 既存のプロジェクトがある場合は、package-lock.jsonとnode_modulesを削除して`pnpm install`を実行
- 環境変数のPATHが正しく設定されていることを確認
- WSLの場合、必要に応じて`~/.bashrc`の代わりに`~/.zshrc`を使用

Next.jsプロジェクトをpnpmで作成する手順をご説明します：

1. create-next-appを使用した初期化：
```bash
pnpm create next-app my-nextjs-project
```

対話式の設定で以下の選択肢が表示されます：
```bash
Would you like to use TypeScript? › Yes
Would you like to use ESLint? › Yes
Would you like to use Tailwind CSS? › Yes
Would you like to use `src/` directory? › Yes
Would you like to use App Router? › Yes
Would you like to customize the default import alias? › No
```

2. プロジェクトディレクトリに移動：
```bash
cd my-nextjs-project
```

3. 開発サーバーの起動：
```bash
pnpm dev
```

追加のパッケージが必要な場合は：
```bash
pnpm add パッケージ名
```

開発用パッケージの場合：
```bash
pnpm add -D パッケージ名
```

この設定で基本的なNext.jsプロジェクトの開発を始められます。


CDKプロジェクトをpnpmで作成する手順をご説明します：



1. 新規ディレクトリの作成と初期化：
```bash
mkdir my-cdk-project
cd my-cdk-project
pnpm init
```

2. 必要なCDK関連パッケージのインストール：
```bash
pnpm add -D aws-cdk aws-cdk-lib constructs
pnpm add -D typescript @types/node
pnpm add -D ts-node
```

3. TypeScript設定ファイルの作成（tsconfig.json）：
```bash
cat << EOF > tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["es2020"],
    "declaration": true,
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    "noUnusedLocals": false,
    "noUnusedParameters": false,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": false,
    "inlineSourceMap": true,
    "inlineSources": true,
    "experimentalDecorators": true,
    "strictPropertyInitialization": false,
    "typeRoots": ["./node_modules/@types"]
  },
  "exclude": ["node_modules", "cdk.out"]
}
EOF
```

4. プロジェクト構造の作成：
```bash
mkdir bin lib
```

5. CDKアプリケーションのエントリーポイント作成（bin/my-cdk-app.ts）：
```typescript
#!/usr/bin/env node
import * as cdk from 'aws-cdk-lib';
import { MyStack } from '../lib/my-stack';

const app = new cdk.App();
new MyStack(app, 'MyStack');
```

6. スタック定義の作成（lib/my-stack.ts）：
```typescript
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';

export class MyStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);
    // リソースの定義をここに追加
  }
}
```

7. package.jsonにスクリプトを追加：
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

8. CDKの初期化：
```bash
pnpm cdk init
```

これでCDKプロジェクトの基本構造が整いました。デプロイする際は：
```bash
pnpm run deploy
```

注意点：
- cdk.jsonファイルが必要な場合は手動で作成
- 必要に応じて.gitignoreも設定
- プロジェクトの要件に応じて追加のパッケージをインストール
