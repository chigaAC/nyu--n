<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>Google Drive プロジェクト作成</title>
</head>
<body>
  <h2>📁 Google Drive プロジェクト作成</h2>
  <input type="text" id="projectName" placeholder="プロジェクト名を入力" />
  <button onclick="init()">開始</button>

  <pre id="log">(ここにログが表示されます)</pre>

  <!-- Google API ライブラリ -->
  <script src="https://apis.google.com/js/api.js"></script>
  <script>
    const clientId = "295167116096-sva04gs0vtr6hvof2r1cfdtlqre4ohpb.apps.googleusercontent.com";
    const apiKey = "AIzaSyBfpmOJjUQLpYdoOBXP4xz-gXIfoHyIiQQ";
    const scopes = "https://www.googleapis.com/auth/drive.file";
    const discoveryDocs = ["https://www.googleapis.com/discovery/v1/apis/drive/v3/rest"];

    const log = msg => {
      const el = document.getElementById("log");
      el.textContent += `\n${msg}`;
      el.scrollTop = el.scrollHeight;
    };

    async function init() {
      log("▶️ 初期化開始...");
      gapi.load("client:auth2", async () => {
        log("✅ gapi.load 完了");
        try {
          await gapi.client.init({ apiKey, clientId, discoveryDocs, scope: scopes });
          await gapi.auth2.getAuthInstance().signIn();
          log("✅ 認証成功");
          createProject();
        } catch (e) {
          log("❌ エラー発生:\n" + (e?.error?.message || e?.message || JSON.stringify(e)));
          console.error(e);
        }
      });
    }

    async function createProject() {
      const name = document.getElementById("projectName").value.trim();
      if (!name) return log("❌ プロジェクト名を入力してください");

      try {
        log(`📁 フォルダ '${name}' を作成中...`);
        const res = await gapi.client.drive.files.create({
          resource: {
            name,
            mimeType: "application/vnd.google-apps.folder"
          },
          fields: "id"
        });
        const projectId = res.result.id;

        // サブフォルダ作成関数
        const createSubfolder = async (subName) => {
          const r = await gapi.client.drive.files.create({
            resource: {
              name: subName,
              parents: [projectId],
              mimeType: "application/vnd.google-apps.folder"
            },
            fields: "id"
          });
          return r.result.id;
        };

        const memoFolderId = await createSubfolder("メモ");
        const embedFolderId = await createSubfolder("埋め込みファイル");

        // map.json の内容作成
        const mapContent = {
          projectName: name,
          folders: {
            memo: memoFolderId,
            embed: embedFolderId
          },
          files: []
        };

        const blob = new Blob([JSON.stringify(mapContent, null, 2)], { type: "application/json" });
        const metadata = {
          name: "map.json",
          parents: [projectId],
          mimeType: "application/json"
        };

        const form = new FormData();
        form.append("metadata", new Blob([JSON.stringify(metadata)], { type: "application/json" }));
        form.append("file", blob);

        const upload = await fetch("https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart", {
          method: "POST",
          headers: new Headers({ Authorization: "Bearer " + gapi.auth.getToken().access_token }),
          body: form
        });

        if (upload.ok) {
          log("✅ プロジェクト作成完了");
        } else {
          log("❌ map.json アップロード失敗");
        }

      } catch (e) {
        log("❌ プロジェクト作成中にエラー:\n" + (e?.error?.message || e?.message || JSON.stringify(e)));
        console.error(e);
      }
    }
  </script>
</body>
</html>
