# amchart4 -> sheetjs -> xlsx

Prototype Pollution 취약점을 패치한 최신 버전의 xlsx를 사용하기 위해 아래와 같이 override를 추가해주었음. (npm에는 더 이상 최신 버전의 xlsx가 배포되지 않아 sheetjs에서 직접 배포한 버전을 사용함)

```json
{
  "overrides": {
    "xlsx": "https://cdn.sheetjs.com/xlsx-0.19.3/xlsx-0.19.3.tgz"
  }
}
```

하지만 이전 버전과 신규 버전의 패키지 진입점(exports)이 다른 부분이 있어 오류가 발생한다. 아래와 같은 경로를 추가해서 오류를 해결함.

```json
{
  "exports": {
    "./dist/xlsx.core.min.js": {
      "import": "./dist/cpexcel.full.mjs",
      "require": "./dist/cpexcel.js",
      "types": "./dist/cpexcel.d.ts"
    }
  }
}
```

수정된 패키지의 버전은 0.19.4로 변경함. 폴리큐브 public repository에 반영했으므로, 아래와 같이 override를 추가해주면 됨.

```json
{
  "overrides": {
    "xlsx": "https://raw.githubusercontent.com/polycube-master/xlsx/main/xlsx-0.19.4.tgz"
  }
}
```
