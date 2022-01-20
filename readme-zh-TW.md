<img src="/assets/jtbp-header-blue.png" width="1920px"/>

<br/>

# 👇 為什麼本指南可以幫助你將測試能力提升到下一個等級

<br/>

## 📗 46+ 個最佳實踐：非常全面且徹底

這是從 A 到 Z 的 JavaScript 及 Node.js 可靠的指南。它為你總結及規劃了市場上大量的部落格文章、書籍及工具。

## 🚢 進階：從基礎向前邁進 10,000 英里

從基礎往前邁進的旅程，包括：在生產(production)環境中測試、變異測試(mutation testing)、以屬性為基礎(property-based)的測試以及許多策略和專業工具。如果你認真閱讀本指南書，你的測試技能可能會高於平均水準。

## 🌐 全端：前端、後端、CI、所有部分

首先了解任何應用程式都通用的測試實踐。然後再深入研究你選擇的領域：前端/UI、後端、CI 或者全部。


<br/>

### 作者 Yoni Goldberg

- A JavaScript & Node.js consultant
- 📗 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com) - My comprehensive online course with more than [10 hours of video](https://www.testjavascript.com), 14 test types and more than 40 best practices
- [Follow me on Twitter](https://twitter.com/goldbergyoni/)

<br/>

### 翻譯 - 以你的語言來閱讀本文

- 🇹🇼[Traditional Chinese](readme-zh-TW.md) - Courtesy of [Yubin Hsu](https://github.com/yubinTW)
- 🇨🇳[Chinese](readme-zh-CN.md) - Courtesy of [Yves yao](https://github.com/yvesyao)
- 🇰🇷[Korean](readme.kr.md) - Courtesy of [Rain Byun](https://github.com/ragubyun)
- 🇵🇱[Polish](readme-pl.md) - Courtesy of [Michal Biesiada](https://github.com/mbiesiad)
- 🇪🇸[Spanish](readme-es.md) - Courtesy of [Miguel G. Sanguino](https://github.com/sanguino)
- 🇧🇷[Portuguese-BR](readme-pt-br.md) - Courtesy of [Iago Angelim Costa Cavalcante](https://github.com/iagocavalcante) , [Douglas Mariano Valero](https://github.com/DouglasMV) and [koooge](https://github.com/koooge)
- 🇫🇷[French](readme-fr.md) - Courtesy of [Mathilde El Mouktafi](https://github.com/mel-mouk)
- Want to translate to your own language? please open an issue 💜

<br/><br/>

## `目錄`

#### [`第 0 章：黃金原則`](#section-0️⃣-the-golden-rule)

一個激發所有人的建議 (1個特殊項目)

#### [`第 1 章：測試剖析`](#section-1-the-test-anatomy-1)

基礎 - 建立乾淨的測試 (12項)

#### [`第 2 章：後端`](#section-2️⃣-backend-testing)

有效率地撰寫後端及微服務的測試 (8項)

#### [`第 3 章：前端`](#section-3️⃣-frontend-testing)

為網頁 UI (包括組件及E2E) 撰寫測試 (11項)

#### [`第 4 章：測量測試的有效程度`](#section-4️⃣-measuring-test-effectiveness)

測量測試的品質 (4項)

#### [`第 5 章：持續整合 (Continuous Integration)`](#section-5️⃣-ci-and-other-quality-measures)

JavaScript 世界的 CI 指南 (9項)

<br/><br/>

# 第 0 章：黃金原則

<br/>

## ⚪️ 0 黃金原則：Design for lean testing

:white_check_mark: **建議：**
測試程式與主要生產環境的程式不同，要把他設計的極其簡單、簡短、具體、扁平、使人愉悅的去使用及學習。一段測試程式應該要可以讓人一眼就看懂其目的。

我們的思考空間被主要的程式邏輯所占滿，並沒有額外的腦容量去處理複雜的東西。如果把其他複雜的程式塞進我們可憐的大腦，將會使得整個團隊的運作變慢，而這些複雜的程式正是用來解決我們需要測試的問題。這也是許多團隊放棄測試的原因。

另一方面，測試是一個友好的助手，一個讓你樂意與他合作、投資小且回報大的助手。科學證明我們有兩套大腦系統：系統 1 用於無須努力的活動，如在空曠的路上開車；系統 2 用於複雜和繁瑣的工作，如計算一道數學式。把你的測試程式設計成如系統 1 一般，當你看著你的測試，要像修改 HTML 文件一樣的簡單，而不是像計算 2 x (17 x 24)。

為了達到這個目標，我們可以選擇具有成本效益和高投資報酬率的的技術、工具和測試目標。只測試需要的內容，努力保持他的靈活性，某些時候甚至得捨棄一些測試來換取靈活性和簡潔性。

![alt text](/assets/headspace.png "We have no head room for additional complexity")

以下大部分的建議衍生自這一原則。

### 準備好了嗎？

<br/><br/>

# 第 1 章：測試剖析

<br/>

## ⚪ ️ 1.1 每個測試的名稱要包含的三個部分

:white_check_mark: **建議：** 一份測試報告應該告訴那些不一定熟悉程式的人，目前應用程式的修訂版本是否符合他們的要求，包括：測試人員、DevOps 工程師和兩年後的你。如果測試能包含這三個需求面的描述，就能很好的實現這一點：

(1) 測試的對象是什麼？ 例如，ProductsService.addNewProduct 這個方法。

(2) 在什麼情況或場景下？ 例如，價格沒有傳給該方法。

(3) 預期的結果是什麼？ 例如，新的產品沒有被批准。

<br/>

❌ **否則：** 一個名叫"新增產品"的測試失敗了。這有確切地告訴你到底是什麼地方出問題嗎？

<br/>

**👇 Note:** 每個項目都會有一個程式範例，有時候還會搭配圖片。
<br/>

<details><summary>✏ <b>程式範例</b></summary>
  
<br/>
  
### :clap: 正例：一個包含這三部分的測試名稱

![](https://img.shields.io/badge/🔨%20Example%20using%20Mocha-blue.svg "Using Mocha to illustrate the idea")

```javascript
// 1. unit under test
describe('Products Service', function() {
  describe('Add new product', function() {
    // 2. scenario and 3. expectation
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});
```

<br/>

### :clap: 正例：一個包含這三部分的測試名稱

![alt text](/assets/bp-1-3-parts.jpeg "A test name that constitutes 3 parts")

</details>

<br/>
<details><summary>© <b>Credits & read-more</b></summary>
  1. <a href='https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html'>Roy Osherove - Naming standards for unit tests</a>
</details>

<br/><br/>

## ⚪ ️ 1.2 以 AAA 模式來建構測試

:white_check_mark: **建議：** 用三個部分來組織你的測試：Arrange 安排、Act 執行、Assert 斷言 (AAA)。依照這個結構，可以確保讀者不用花費腦力去理解你的測試。

第一個 A - Arrange 安排：所有使系統達到測試所要模擬的情境的程式。這可能包含實體化某個待測單元的建構子、新增 DB 的資料、mocking/stubbing 物件和其他準備程式。

第二個 A - Act 執行：執行測試單元。通常為一行程式。

第三個 A - Assert 斷言：確保得到的值符合期待。通常為一行程式。

<br/>

❌ **否則：** 你不僅需要花很多時間去理解主要程式，而且本應是最簡單的部分 - 測試，也會讓你腦力耗盡。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：以 AAA 模式來建構測試

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest") ![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
describe("Customer classifier", () => {
  test("When customer spent more than 500$, should be classified as premium", () => {
    // Arrange
    const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
    const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });

    // Act
    const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);

    // Assert
    expect(receivedClassification).toMatch("premium");
  });
});
```

<br/>

### :thumbsdown: 反例：沒有分隔、一大坨、難以理解

```javascript
test("Should be classified as premium", () => {
  const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
  const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });
  const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);
  expect(receivedClassification).toMatch("premium");
});
```

</details>

<br/><br/>

## ⚪ ️1.3 用產品語言來描述預期：使用 BDD 風格的斷言

:white_check_mark: **建議：** 使用聲明的方式撰寫測試，可以使讀者無腦的 get 到重點。如果你的程式使用各種條件邏輯包起來，會增加讀者的理解難度。因此，我們應該盡量使用類似人類語言的描述與言如 ```expect``` 或 ```should``` 而不是自己寫程式。如果 Chai 或 Jest 沒有你想要用的斷言，且這個斷言可以被頻繁的重複利用的話，可以考慮  [擴充 Jest 的匹配器 (Jest)](https://jestjs.io/docs/en/expect#expectextendmatchers) 或是寫一個 [客製化的 Chai 插件](https://www.chaijs.com/guide/plugins/)。

<br/>

❌ **否則：** 團隊的測試會越寫越少，且會用 .skip() 把討厭的測試略過。

<br/>

<details><summary>✏ <b>程式範例</b></summary><br/>

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai") ![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

### :thumbsdown: 反例：讀者必須快速的看完冗長且複雜的程式碼，才能理解該測試的目的

```javascript
test("When asking for an admin, ensure only ordered admins in results", () => {
  // assuming we've added here two admins "admin1", "admin2" and "user1"
  const allAdmins = getUsers({ adminOnly: true });

  let admin1Found,
    adming2Found = false;

  allAdmins.forEach(aSingleUser => {
    if (aSingleUser === "user1") {
      assert.notEqual(aSingleUser, "user1", "A user was found and not admin");
    }
    if (aSingleUser === "admin1") {
      admin1Found = true;
    }
    if (aSingleUser === "admin2") {
      admin2Found = true;
    }
  });

  if (!admin1Found || !admin2Found) {
    throw new Error("Not all admins were returned");
  }
});
```

<br/>

### :clap: 正例：快速瀏覽以下的聲明式測試非常輕鬆

```javascript
it("When asking for an admin, ensure only ordered admins in results", () => {
  // assuming we've added here two admins
  const allAdmins = getUsers({ adminOnly: true });

  expect(allAdmins)
    .to.include.ordered.members(["admin1", "admin2"])
    .but.not.include.ordered.members(["user1"]);
});
```

</details>

<br/><br/>

## ⚪ ️ 1.4 堅持黑箱測試：只測試公開方法

:white_check_mark: **建議：** 測試內部邏輯是無意義且浪費時間的。如果你的程式/API 回傳了正確的結果，你真的需要花三個小時的時間去測試它內部究竟如何實現的，並且在之後維護這一堆脆弱的測試嗎？每當測試一個公開方法時，其私有方法的實作也會被隱性地測試，只有當存在某個問題(例如錯誤的輸出)時測試才會中斷。這種方法也稱為 ```行為測試```。另一方面，如果你測試內部方法 (白箱方法) — 你的關注點將從組件的輸出結果轉移到具體的實作細節上，如果某天內部邏輯改變了，即使結果依然正確，你也要花精力去維護之前的測試邏輯，這無形中增加了維護成本。
<br/>

❌ **否則：** 你的測試會像[狼來了](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf)一樣，總是叫喚著出問題了 (例如一個因為內部變數名稱改變而導致的測試失敗)。不出所料，人們很快就會開始忽視 CI 的通知，直到某天，一個真正的 bug 被忽視...

<br/>
<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :thumbsdown: 反例：一個無腦測試內部方法的測試

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha & Chai")

```javascript
class ProductService {
  // this method is only used internally
  // Change this name will make the tests fail
  calculateVATAdd(priceWithoutVAT) {
    return { finalPrice: priceWithoutVAT * 1.2 };
    // Change the result format or key name above will make the tests fail
  }
  // public method
  getPrice(productId) {
    const desiredProduct = DB.getProduct(productId);
    finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
    return finalPrice;
  }
}

it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
  // There's no requirement to allow users to calculate the VAT, only show the final price. Nevertheless we falsely insist here to test the class internals
  expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});
```

</details>

<br/><br/>

## ⚪ ️ ️1.5 使用正確的測試替身 (Test Double)：避免總是使用 stub 和 spy

:white_check_mark: **建議：** 測試替身是把雙刃劍，他們在提供巨大價值的同時，耦合了應用的內部邏輯 ([一篇關於測試替身的文章: mocks vs stubs vs spies](https://martinfowler.com/articles/mocksArentStubs.html)) 在使用測試替身前，問自己一個很簡單的問題：我是用它來測試需求文件中定義的可見的功能或者可能可見的功能嗎？如果不是，那就可能是白盒測試了。

舉例來說，如果你想測試你的應用程式在支付服務當機時的預期行為，你可以 stub 支付服務並觸發一些"沒有回應"的回傳行為，以確保被測試的單元回傳正確的值。這可以測試特定場景下應用程式的行為、回應及輸出結果。你也可以使用一個 spy 來斷言當服務當機時是否有發送電子郵件 - 這又是一個針對可能出現在需求文件中行為的檢查 ("如果無法儲存付款資訊，發送電子郵件")。反過來說，如果你 mock 的支付服務，能確保它被正確呼叫並傳入正確的 JavaScript 型別，那麼你的測試重點是內部的邏輯，它與應用程式的功能關係不大，而且可能會經常變化。

<br/>

❌ **否則：** 任何程式的重構都會需要程式中所有的 mock 進行相對應的更新。測試變成了一種負擔，而不是一個助力。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :thumbsdown: 反例：關注內部實作的 mock

![](https://img.shields.io/badge/🔧%20Example%20using%20Sinon-blue.svg "Examples with Sinon")

```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
  // Assume we already added a product
  const dataAccessMock = sinon.mock(DAL);
  // hmmm BAD: testing the internals is actually our main goal here, not just a side-effect
  dataAccessMock
    .expects("deleteProduct")
    .once()
    .withArgs(DBConfig, theProductWeJustAdded, true, false);
  new ProductService().deletePrice(theProductWeJustAdded);
  dataAccessMock.verify();
});
```

<br/>

### :clap: 正例：Spy 專注於測試需求，但身為一個 side effect，無可避免地會接觸到內部程式結構

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
  // Assume we already added here a product
  const spy = sinon.spy(Emailer.prototype, "sendEmail");
  new ProductService().deletePrice(theProductWeJustAdded);
  // hmmm OK: we deal with internals? Yes, but as a side effect of testing the requirements (sending an email)
  expect(spy.calledOnce).to.be.true;
});
```

</details>

<br/><br/>

## 📗 想要透過影片來學習這些做法嗎？

### 歡迎來我的線上課程網站 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/><br/>

## ⚪ ️1.6 不要 "foo", 使用真實的資料

:white_check_mark: **建議：** 生產環境中的 bug 通常是在一些特殊或者意外的輸入下出現的 — 所以測試的輸入資料越真實，越容易在早期抓住問題。使用現有的一些函式庫（比如 [Faker](https://www.npmjs.com/package/faker)）去造"假"真實數據來模擬生產環境數據的多樣性和形式。比如，這些函示庫可以產生真實的電話號碼、用戶名稱、信用卡、公司名稱等等。你還可以創建一些測試(在單元測試之上，而不是替代)生產隨機 fakers 數據來擴充你的測試單元，甚至從生產環境中導入真實的資料。如果想要更進階的話，請看下一個項目：基於屬性的測試 (property-based testing)。
<br/>

❌ **否則：** 你要部屬的程式都在 "foo" 之類的輸入值中正確的通過測試，結果上線之後收到像是 ```@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA``` 之類的輸入值後掛掉了。 

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :thumbsdown: 反例: 一個測試案例使用非真實資料去通過測試

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
const addProduct = (name, price) => {
  const productNameRegexNoSpace = /^\S*$/; // no white-space allowed

  if (!productNameRegexNoSpace.test(name)) return false; // this path never reached due to dull input

  // some logic here
  return true;
};

test("Wrong: When adding new product with valid properties, get successful confirmation", async () => {
  // The string "Foo" which is used in all tests never triggers a false result
  const addProductResult = addProduct("Foo", 5);
  expect(addProductResult).toBe(true);
  // Positive-false: the operation succeeded because we never tried with long
  // product name including spaces
});
```

<br/>

### :clap:正例：使用隨機產生的真實資料來輸入

```javascript
it("Better: When adding new valid product, get successful confirmation", async () => {
  const addProductResult = addProduct(faker.commerce.productName(), faker.random.number());
  // Generated random input: {'Sleek Cotton Computer',  85481}
  expect(addProductResult).to.be.true;
  // Test failed, the random input triggered some path we never planned for.
  // We discovered a bug early!
});
```

</details>

<br/><br/>

## ⚪ ️ 1.7 Property-based testing 基於屬性的測試：測試輸入的多種組合

:white_check_mark: **建議：** 通常我們只會選擇少部分的輸入樣本去做測試。 即使是使用了上一項提到的工具去模擬真實數據，我們也只覆蓋到了一部分輸入的組合 (```method('', true, 1)```, ```method('string', false , 0)```)。然而在生產環境中，一個擁有 5 個參數的 API，可能會遇到上千種排列組合的輸入，而其中的某一種可能會把你的程式搞掛（可參考 [Fuzz Testing](https://en.wikipedia.org/wiki/Fuzzing)）。

如何撰寫一個測試，可以自動發送 1000 種不同輸入的排列組合，並捕捉到使我們的程式不能正確回傳的輸入？基於屬性的測試 (Property-based testing) 就是這樣一種技術：透過發送所有可能的輸入組合到你的測試單元中，它增加了發現 bug 的可能性。

例如，給定一個方法 — ```addNewProduct(id, name, isDiscount)``` — 函示庫將使用許多 ```(number, string, boolean)``` 的組合來呼叫這個方法，比如 ```(1, 'iPhone', false)```，```(2, 'Galaxy', true)```。您可以使用您喜歡的測試運行器(Mocha、Jest等)，使用 [js-verify](https://github.com/jsverify/jsverify) 或者 [testcheck](https://github.com/leebyron/testcheck-js) (文件寫得比較好) 來執行基於屬性的測試。

更新：Nicolas Dubien 在下面的回復中建議使用 [fast-check](https://github.com/dubzzz/fast-check#readme)，它似乎提供了更多的功能，且有被積極維護。

<br/>

❌ **否則：** 你無意中選擇的測試輸入只涵蓋到運作正常的程式片段。不幸的是，他沒有發現真正的錯誤，這也降低了把測試當作發現錯誤的工具的成效。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例： 使用 fast-check 來測試許多的輸入組合

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
import fc from "fast-check";

describe("Product service", () => {
  describe("Adding new", () => {
    // this will run 100 times with different random properties
    it("Add new product with random yet valid properties, always successful", () =>
      fc.assert(
        fc.property(fc.integer(), fc.string(), (id, name) => {
          expect(addNewProduct(id, name).status).toEqual("approved");
        })
      ));
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.8 如果需要，只使用簡短的行內快照 (inline snapshots)

:white_check_mark: **建議：** 如果你需要進行 快照測試 ([snapshot testing](https://jestjs.io/docs/en/snapshot-testing))，只使用短而集中的快照 (如3~7行)，該快照是測試程式的一部份，而不是在外部文件中。保持好這一原則，將會確保你的測試的自我解釋性且不會那麼脆弱。

另一方面，"classic snapshots"的教學和工具鼓勵將大文件 (如組件的渲染結果、API 的 JSON 結果) 存儲在一些外部媒介上，並確保每次測試運行時，將收到的結果與保存的版本進行比較。舉個例子，這將會隱性地將我們的測試與包含3000個數值的1000行內容耦合在一起，而測試者從未閱讀和推理過這些數據。為什麼這樣是不對的？ 這樣做，將會有1000個原因讓你的測試失敗 - 只要有一行改變，快照比對就會 fail，而這可能會經常發生。多頻繁？當有每一個空格、註解或一點 CSS/HTML 的變化。不僅如此，測試名稱也不會提供關於失敗的線索，因為它只是檢查這1000行是否有變化，而且它還鼓勵測試者去接受一個他無法檢查和驗證的大文件作為期望的結果。所有這些都是測試目標不明確、測試目標過多的症狀。

值得注意的是，在少數情況下，大型的外部快照是可以接受的 - 當斷言的對象是 schema 而不是所有內容時 (提取出要的值並專注在某個欄位上)，或者當收到的文件內容幾乎不會改變時。 

<br/>

❌ **否則：** 一個 UI 的測試失敗了。程式看起來是對的，畫面上也完美渲染了每個像素，但怎麼了？ 你的測試程式發現收到的內容與期望的不同，或許只是多了一個空格...

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :thumbsdown: 反例： 將看不到的 2000 行程式耦合進我們的測試案例中

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
it("TestJavaScript.com is renderd correctly", () => {
  // Arrange

  // Act
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  // Assert
  expect(receivedPage).toMatchSnapshot();
  // We now implicitly maintain a 2000 lines long document
  // every additional line break or comment - will break this test
});
```

<br/>

### :clap: 正例：期望是可見且集中的

```javascript
it("When visiting TestJavaScript.com home page, a menu is displayed", () => {
  // Arrange

  // Act
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  // Assert

  const menu = receivedPage.content.menu;
  expect(menu).toMatchInlineSnapshot(`
<ul>
<li>Home</li>
<li> About </li>
<li> Contact </li>
</ul>
`);
});
```

</details>

<br/><br/>

## ⚪ ️1.9 避免使用全域的 test fixtures 或 seeds，而是放進每個測試中

:white_check_mark: **建議：** 參照黃金原則，每個測試需要在它自己的 DB 中進行操作避免互相污染。但現實中，這條規則經常被打破：為了性能的提升而在執行測試前初始化全域資料庫 (也被稱為"[test fixture](https://en.wikipedia.org/wiki/Test_fixture)")。儘管性能很重要，但是它可以通過後面講的「組件測試」來做取捨。為了減輕複雜度，我們可以在每個測試中只初始化自己需要的數據。除非性能問題真的非常嚴重，那還是可以做一定程度的妥協 - 僅在全域放不會改變的數據 (比如 query)。

<br/>

❌ **否則：** 有一些測試 fail 了，團隊花了許多時間後發現，只是因為兩個測試同時改變了同一個 seed。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :thumbsdown: 反例：測試案例之間不是獨立的。而是相依於全域的 DB 資料

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
before(async () => {
  // adding sites and admins data to our DB. Where is the data? outside. At some external json or migration framework
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  // I know that site name "portal" exists - I saw it in the seed files
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  // I know that site name "portal" exists - I saw it in the seed files
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); // Failure! The previous test change the name :[
});

```

<br/>

### :clap: 正例：每個測試案例只操作他自己的資料

```javascript
it("When updating site name, get successful confirmation", async () => {
  // test is adding a fresh new records and acting on the records only
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });

  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");

  expect(updateNameResult).to.be(true);
});
```

</details>

<br/>

## ⚪ ️ 1.10 不要 catch 錯誤，expect 他們

:white_check_mark: **建議：** 當你要測試一些輸入是否有觸發錯誤時，使用 ```try-catch-finally``` 來檢查他是否會進入到 catch 區塊，看起來沒什麼問題。但會變成一個笨拙且冗長的測試案例 (如下面程式範例)，他會隱藏簡單的測試意圖和預期的結果。

一個更為優雅的作法是使用專用的單行斷言：如 Chai 中的 ```expect(method).to.throw``` 或是 Jest 中的 ```expect(method).toThrow()```。必須要確保這個 expection 包含某個預期的 error type，如果只得到一個通用的錯誤型態，那應用程式將無法表明更多訊息給使用者。

<br/>

❌ **否則：** 從測試報告 (如 CI 報告) 中要看出哪裡有錯會非常困難。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :thumbsdown: 反例：一個很長的測試案例，嘗試使用 ```try-catch``` 來斷言錯誤

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

```javascript
it("When no product name, it throws error 400", async () => {
  let errorWeExceptFor = null;
  try {
    const result = await addNewProduct({});
  } catch (error) {
    expect(error.code).to.equal("InvalidInput");
    errorWeExceptFor = error;
  }
  expect(errorWeExceptFor).not.to.be.null;
  // if this assertion fails, the tests results/reports will only show
  // that some value is null, there won't be a word about a missing Exception
});
```

<br/>

### :clap: 正例：一個容易閱讀及被了解的 expection，甚至能被 QA 或 PM 理解

```javascript
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

</details>

<br/><br/>

## ⚪ ️ 1.11 為測試案例打上標籤

:white_check_mark: **建議：** 不同的測試需要在不同的情境下執行：快速冒煙測試、無 IO 的測試、開發者儲存或提交檔案的測試、送出一個 PR 後的 end-to-end 測試等等。 可以用一些 ```#cold``` ```#api``` ```#sanity``` 之類的標籤來標註這些測試，這樣就可以在測試時只執行特定的子集合。例如在 Mocha 中可以這樣來執行：```mocha -- grep 'sanity'```。
<br/>

❌ **否則：** 執行所有測試案例，包括執行大量查詢 DB 的測試，開發者做的任何微小的變更都需要花很長的時間去跑完所有的測試，將會導致開發者不想再執行測試。

<br/>

<details><summary>✏ <b>程式範例：</b></summary>

<br/>

### :clap: 正例：將測試案例標記為 '#cold-test' 讓執行測試的人可以只執行速度快的測試案例 (cold 指的是沒有 IO 的快速測試，甚至可以在開發人員打字時頻繁地執行)

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
// this test is fast (no DB) and we're tagging it correspondigly
// now the user/CI can run it frequently
describe("Order service", function() {
  describe("Add new order #cold-test #sanity", function() {
    test("Scenario - no currency was supplied. Expectation - Use the default currency #sanity", function() {
      // code logic here
    });
  });
});
```

</details>

<br/><br/>

## ⚪ ️ 1.12 把測試案例進行至少兩個層次的分類

:white_check_mark: **建議：** 對測試案例套用一些結構，讓每個看到這個測試案例的人都可以很容易得理解需求 (測試是最好的文件) 和正在測試的各種情境。一個常見的方法是在測試上方寫至少兩個用來"描述"的區塊：第一個是測試單元的名稱，第二個是額外的分類名稱，如情境或自定義的類別 (參考下面的程式範例和畫面輸出)。這樣的做法也會大幅的改善測試報告的呈現。讀者將會很容易的推斷出測試的類別，讀懂該測試的內容並與失敗的測試關聯起來。此外，對開發者來說，瀏覽這一連串的測試也變得更加容易。有許多額外的結構也是可以考慮使用的，像是 [given-when-then](https://github.com/searls/jasmine-given) 或 [RITE](https://github.com/ericelliott/riteway)。

<br/>

❌ **否則：** 當看到一份毫無結構且數量眾多的測試報告時，讀者只能透過粗略地閱讀整份報告來總結，並將失敗的錯誤案例關聯起來。思考一個情況，當100個測試案例中有7個失敗時，看一個分層結構良好的測試報告與看一個扁平的測試結果清單相比，那些錯誤的測試案例很有可能都在同一個流程或分類底下，讀者將可以很快的推斷出錯誤的地方或看出哪部分是他們失敗的原因。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：利用測試案例的名稱和情境來組織，可以產生良好的測試報告，如下所示

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
// Unit under test
describe("Transfer service", () => {
  // Scenario
  describe("When no credit", () => {
    // Expectation
    test("Then the response status should decline", () => {});

    // Expectation
    test("Then it should send email to admin", () => {});
  });
});
```

![alt text](assets/hierarchical-report.png)

<br/>

### :thumbsdown: 反例：扁平的測試列表會使讀者很難去看懂 user story 和失敗的測試之間的關係

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Mocha")

```javascript
test("Then the response status should decline", () => {});

test("Then it should send email", () => {});

test("Then there should not be a new transfer record", () => {});
```

![alt text](assets/flat-report.png)

<br/>

</details>

<br/><br/>

## ⚪ ️1.13 其他通用且良好的測試習慣

:white_check_mark: **建議：** 本篇文章的重點是與 NodeJS 相關的測試建議或至少可以用 NodeJS 來舉例說明的內容。然而，這裡有幾個與 NodeJS 無關的建議，且是眾所皆知的。

學習並實現 [TDD原則](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/) - 他對許多人來說非常有價值，但如果他不適合你的風格，不要被嚇到，不是只有你這樣。試著在寫程式之前使用 [red-green-refactor](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html) 的風格來撰寫測試，並確保每個測試案例只檢查一個測試目標。當你發現一個 bug 時，在修復它之前先新增一個可以檢測到它的測試案例，讓每個測試案例在變綠之前至少失敗一次，接著快速撰寫簡單的程式讓這個測試通過 - 然後逐步重構這些程式到可以上 production 的水準，避免對環境 (如路徑或作業系統等) 有任何相依性。

<br/>

❌ **否則：** 你會錯過這數十年來的智慧結晶

<br/><br/>

# 第 2 章：後端測試

## ⚪ ️2.1  豐富您的測試組合：不局限於單元測試和測試金字塔

:white_check_mark: **建議：** 雖然 [測試金字塔](https://martinfowler.com/bliki/TestPyramid.html) 已經有超過十年的歷史了，但他仍然是個很好的模型，他提出了三種測試類型，並影響了大多數開發者的測試策略。與此同時，大量閃亮的新測試技術出現了，並隱藏在測試金字塔的陰影下。考慮到近十年來我們所看到的所有巨變 (Microservices, cloud, serverless)，這個非常老的模型是否仍能適用於所有類型的應用？測試界不應該考慮新的測試技術嗎？ 

不要誤會，在 2019 年，測試金字塔、TDD、單元測試仍然是強大的技術，且對於大多數應用仍是最佳選擇。但是像其他模型一樣，儘管它有用，但是一定[會在某些時候出問題](https://en.wikipedia.org/wiki/All_models_are_wrong)。例如，我們有一個 IoT 的應用程式，將許多事件傳入一個 Kafka/RabbitMQ 這樣的 message-bus 中，然後這些事件流入資料庫並被經由 UI 來做查詢。我們真的需要花費 50% 的測試預算去為這個幾乎沒有邏輯的中心化的整合應用程式寫單元測試嗎？隨著應用類型 (bots, crypto, Alexa-skills) 的多樣增長，測試金字塔可能將不再是某些場景的最佳選擇了。

是時候豐富你的測試組合並了解更多的測試類型了（下一節會給你一些小建議），這些類似於測試金字塔的思維模型與你所面臨的現實問題會更加匹配（"嘿，我們的 API 掛了，我們來寫 consumer-driven contract testing 吧！"）。讓您的測試多樣化，比如建立基於風險分析的檢查模型 — 評估可能出現問題的地方，並提供一些預防措施以減輕這些潛在風險。

需要注意的是：軟體世界中的 TDD 模型面臨兩個極端的態度，一些人鼓吹到處使用它，另一些人則認為它是魔鬼。每個說絕對的人都是錯的 :] 

<br/>

❌ **否則：** 你將錯過一些超高 CP 值的工具，比如 Fuzz、lint、mutation，這些工具只需 10 分鐘設定就能為你提供許多好處。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：Cindy Sridharan 在她的文章 "Testing Microservices — the sane way" 中提出了一個豐富的測試組合

![alt text](assets/bp-12-rich-testing.jpeg "Cindy Sridharan suggests a rich testing portfolio in her amazing post ‘Testing Microservices — the sane way’")

<strong class="markup--strong markup--p-strong">☺️Example: </strong><a href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtube" data-href="https://www.youtube.com/watch?v=-2zP494wdUY&amp;feature=youtu.be" class="markup--anchor markup--p-anchor" rel="nofollow noopener" target="_blank">[YouTube: “Beyond Unit Tests: 5 Shiny Node.JS Test Types (2018)” (Yoni Goldberg)](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)</a>

<br/>

![alt text](assets/bp-12-Yoni-Goldberg-Testing.jpeg "A test name that constitutes 3 parts")

</details>

<br/><br/>

## ⚪ ️2.2 組件化測試可能是最有效的利器

:white_check_mark: **建議：** 應用程式中的每個單元測試僅能覆蓋整個程式的一小部分，要覆蓋全部會非常麻煩，而端到端測試可以很輕鬆地覆蓋大量區域，但是比較脆弱而且很慢。何不找一個平衡點：寫一些比單元測試大，但是比端到端測試小的測試。組件測試是測試世界的一顆遺珠 — 它找到了兩個模式的最佳平衡點：不錯的性能和使用 TDD 模式的可能性與真實且強大的覆蓋率。

組件測試關注於微服務"單元"，他們針對 API 來做事，不 mock 任何屬於微服務本身的東西（像是真實的 DB，甚至是該 DB 的 in-memory 版本）但是 stub 所有外部的東西，像是呼叫其他的微服務。藉由這種方式，我們可以測試我們部署的部分，由外而內地覆蓋應用程式，可以節省大量時間並獲得信心。

<br/>

❌ **否則：** 你可能花了好幾天來寫單元測試，卻發現只得到了 20% 的覆蓋率。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：使用 Supertest 來測試 Express API (快速且覆蓋多個層次)

![](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Examples with Mocha")

![alt text](assets/bp-13-component-test-yoni-goldberg.png " [Supertest](https://www.npmjs.com/package/supertest) allows approaching Express API in-process (fast and cover many layers)")

</details>

<br/><br/>

## ⚪ ️2.3 利用 contract tests 來確保新的 release 不會破壞 API 的使用

:white_check_mark: **建議：** 你的微服務有許多客戶，而你為了兼容性而運行著很多種版本 (keeping everyone happy)。當你改了某些程式後 "砰！"，某些使用該服務的重要客戶生氣了。伺服端要滿足所有客戶的期望是非常困難的 - 另一方面，客戶端無法執行任何測試，因為 release 的日期是伺服端決定的。

[Consumer-driven contracts and the framework PACT](https://docs.pact.io/) 誕生了，它以一種破壞性的方式規範了這一流程 — 不再由伺服端定義測試計劃，而是客戶端決定伺服端的測試！ PACT 可以記錄客戶端的期望並存放在一個共享的位置 — 中間人（Broker），伺服端可以 pull 下這些期望並利用 PACT 的函示庫在所有版本中檢測是否有被破壞的契約，也就是客戶端的期望沒有被滿足。通過這種方式，所有 伺服端-用戶端 沒對好的 API 將會在 build/CI 階段被發現，從而減少你的煩惱。
<br/>

❌ **否則：** 所有的變更都將會造成繁瑣的人工測試，導致開發者害怕部屬

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：

![](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "Examples with PACT")

![alt text](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪ ️2.4 單獨測試你的 middlewares

:white_check_mark: **建議：** 許多人拒絕測試 middleware，因為它們只佔系統的一小部分而且相依於真實的 Express server。這兩個原因都不正確 — middleware 雖然小，但是影響著所有或至少大部分請求，而且可以被簡單地作為純函數測試 (參數為 ```{req,res}``` 的 JavaScript 物件)。要測試 middleware 函數，只需要呼叫它，並且監看 ([如使用 Sinon](https://www.npmjs.com/package/sinon)) 與 ```{req,res}``` 的互動來確保函數有執行正確的行為。 [node-mock-http](https://www.npmjs.com/package/node-mocks-http) 函示庫則更進一步：它還監聽了 ```{req,res}``` 物件的行為。例如，它可以斷言 res 物件上的 http 狀態是否符合預期。(看下面的程式範例)
<br/>

❌ **否則：** Express middlewares 的 bug === 所有或大部分 request 的 bug

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：單獨測試 middleware，不發出網路請求或啟動整個 Express 伺服器

![](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Examples with Jest")

```javascript
// the middleware we want to test
const unitUnderTest = require("./middleware");
const httpMocks = require("node-mocks-http");
// Jest syntax, equivelant to describe() & it() in Mocha
test("A request without authentication header, should return http status 403", () => {
  const request = httpMocks.createRequest({
    method: "GET",
    url: "/user/42",
    headers: {
      authentication: ""
    }
  });
  const response = httpMocks.createResponse();
  unitUnderTest(request, response);
  expect(response.statusCode).toBe(403);
});
```

</details>

<br/><br/>

## ⚪ ️2.5 使用靜態分析工具來測量與重構

:white_check_mark: **建議：** 使用靜態分析工具可以幫助你客觀地提升程式品質並保持可維護性。你可以將靜態分析工具放在你的 CI 中。除了普通的 linting 外，它的主要賣點是查看多個檔案的上下文來檢查程式碼品質 (例如：發現程式有沒有重複定義的地方)、執行進階的分析 (例如：程式複雜度) 以及追蹤 code issue 的歷史和進度。有兩個工具供你使用：[SonarQube](https://www.sonarqube.org/) (6,300+ [stars](https://github.com/SonarSource/sonarqube)) 和 [Code Climate](https://codeclimate.com/) (2,300+ [stars](https://github.com/codeclimate/codeclimate))。

Credit: <a href="https://github.com/TheHollidayInn" data-href="https://github.com/TheHollidayInn" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">[Keith Holliday](https://github.com/TheHollidayInn)</a>

<br/>

❌ **否則；** 程式碼的品質過差，再新的函式庫或功能都無法拯救你的 bug 和性能

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：CodeClimate，一個可以發現複雜方法的商業工具

![](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "Examples with CodeClimate")

![alt text](assets/bp-16-yoni-goldberg-quality.png "CodeClimate, a commercial tool that can identify complex methods:")

</details>

<br/><br/>

## ⚪ ️ 2.6 檢查你對 Node 相關渾沌的準備工作

:white_check_mark: **建議：** 奇怪的是，大部分的軟體測試都只專注在邏輯和資料層面，但最重要且很難被緩解的，是那些基礎設施的問題。例如，你有測試過當你的程序記憶體過載、伺服器或程序死掉時的表現嗎？或者你的監控系統可以檢測到 API 的回應時間慢了 50% 嗎？為了測試與減輕類似的問題，Netflix 設立了混沌工程 [Chaos engineering](https://principlesofchaos.org/)。它的目的是提供意識、框架及工具來測試我們的應用程式對於混沌問題的彈性。比如，最著名的工具之一，渾沌猴子 [the chaos monkey](https://github.com/Netflix/chaosmonkey)，他會隨機地殺掉服務以確保我們的服務仍然可以提供服務給客戶，而不是僅依賴一個單獨的伺服器 (Kubernetes 也有一個 [kube-monkey](https://github.com/asobti/kube-monkey) 用來殺掉 pods)。這些工具都是作用在伺服器/平台面，但如果你想測試及產生單純的 Node 渾沌，比如檢查你的 Node 程序如何處理未知錯誤、未知的 promise rejection、v8 使用的記憶體超過 1.7GB 的限制以及當 event loop 卡住後你的 UX 是否仍然可以正常運行？為了解決上面提到的問題， [node-chaos](https://github.com/i0natan/node-chaos-monkey) 提供了各種 Node 相關的渾沌。 

<br/>

❌ **否則：** 莫非定律一定會擊中你的產品，無可避免的

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例：Node-chaos 可以產生所有類型的 Node.js 問題，因此您可以測試您的應用程序對於渾沌的適應能力

![alt text](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "Node-chaos can generate all sort of Node.js pranks so you can test how resilience is your app to chaos")

</details>

<br/><br/>

# 第 3 章：前端測試

## ⚪ ️ 3.1 將 UI 與功能分離

:white_check_mark: **建議：** 當專注於測試組件邏輯時，UI 的細節就變成了應該被剔除的雜音，這樣您的測試目標就可以集中在資料面上。實際上，提取出程式中所需的資料，將降低與畫面的耦合，僅對單純的資料 (與 HTML/CSS 等圖形細節相比) 進行斷言，並停用會拖慢速度的動畫。您應該要試著避免畫面的渲染，僅測試 UI 後面的部分 (例如，服務、動作、存儲)，但這將導致測試與實際情況不相符，「正確的資料根本無法呈現在 UI 上」這種問題就無法發現。

<br/>

❌ **否則：** 你的測試可能花了 10ms 就準備好資料，但因為一些無關緊要的花俏動畫，讓整個測試案例持續了 500ms。(100個測試 = 1分鐘)

<br/>

<details><summary>✏ <b>程式範例：</b></summary>

<br/>

### :clap: 正例；分離 UI 的細節

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
test("When users-list is flagged to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Extract the data from the UI first
  const allRenderedUsers = getAllByTestId("user").map(uiElement => uiElement.textContent);
  const allRealVIPUsers = allUsers.filter(user => user.vip).map(user => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); // compare data with data, no UI here
});
```

<br/>

### :thumbsdown: 反例：混雜了 UI 與資料的斷言

```javascript
test("When flagging to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Mix UI & data in assertion
  expect(getAllByTestId("user")).toEqual('[<li data-test-id="user">John Doe</li>]');
});
```

</details>

<br/><br/>

## ⚪ ️ 3.2 使用不易改變的屬性來查询 HTML 元素

:white_check_mark: **建議：** 使用不太容易受畫面變更而影響的屬性來查詢 HTML 元素 (例如 form label，而不是 CSS selector)。如果指定的元素沒有這樣的屬性，則創建一個專用的測試屬性，如 `test-id-submit-button`。這樣做不僅可以確保您的功能/邏輯測試不會因為外觀變化而中斷，而且整個團隊可以清楚地看到，測試案例使用了這個元素和屬性，不應該刪除它。 

<br/>

❌ **否則：** 假設你想要測試一個跨越許多組件、邏輯和服務的登入功能，一切都設置得很完美 - stub、spy、Ajax 的呼叫都是隔離的。看似一切都很完美，但卻發現測試失敗了，因為開發者將 div 的 class 從 `thick-border` 改為 `thin-border`。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例： 使用專用的 attribute 來查詢元素來進行測試

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React")

```html
// the markup code (part of React component)
<h3>
  <Badge pill className="fixed_badge" variant="dark">
    <span data-test-id="errorsLabel">{value}</span>
    <!-- note the attribute data-test-id -->
  </Badge>
</h3>
```

```javascript
// this example is using react-testing-library
test("Whenever no data is passed to metric, show 0 as default", () => {
  // Arrange
  const metricValue = undefined;

  // Act
  const { getByTestId } = render(<dashboardMetric value={undefined} />);

  expect(getByTestId("errorsLabel").text()).toBe("0");
});
```

<br/>

### :thumbsdown: 反例： 依靠於 CSS attributes

```html
<!-- the markup code (part of React component) -->
<span id="metric" className="d-flex-column">{value}</span>
<!-- what if the designer changes the classs? -->
```

```javascript
// this exammple is using enzyme
test("Whenever no data is passed, error metric shows zero", () => {
  // ...

  expect(wrapper.find("[className='d-flex-column']").text()).toBe("0");
});
```

</details>

<br/>

## ⚪ ️ 3.3 如果可以，使用真實且完全渲染的組件來進行測試

:white_check_mark: **建議：** 只要尺寸合適，像使用者那樣從外部測試你的組件，完全渲染 UI，對其進行操作，並斷言對那些 UI 的行為是否符合預期。避免各種 mock、partial 和 shallow rendering - 這樣做可能會因為缺乏細節而導致有未捕捉到的 bug，而且由於測試會擾亂內部的結構而使得維護變得更加困難 (參考 堅持黑箱測試)。如果其中一個子組件明顯拖慢速度 (如 動畫) 或很難去設定，可以考慮使用假的組件去替換它。

綜上所說，需要注意的是：這種技術適用於包含合理大小子組件的中小型組件。完全渲染一個有太多子組件的組件會讓他很難被看出失敗的原因 (root cause analysis)，而且可能會非常慢。在這種情況下，可以對那些很肥的父組件撰寫少量的測試，並對其子組件多寫幾個測試。

<br/>

❌ **否則：** 呼叫組件的私有方法來測試組件的內部狀態。後續重構組件時你必須重構所有測試。你真的有能力進行這種程度的維護嗎？

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例： 操作一個充分渲染的真實組件

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20Enzyme-blue.svg "Examples with Enzyme")

```javascript
class Calendar extends React.Component {
  static defaultProps = { showFilters: false };

  render() {
    return (
      <div>
        A filters panel with a button to hide/show filters
        <FiltersPanel showFilter={showFilters} title="Choose Filters" />
      </div>
    );
  }
}

// Examples use React & Enzyme
test("Realistic approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = mount(<Calendar showFilters={false} />);

  // Act
  wrapper.find("button").simulate("click");

  // Assert
  expect(wrapper.text().includes("Choose Filter"));
  // This is how the user will approach this element: by text
});
```

### :thumbsdown: 反例： 使用 shallow rendering 來測試

```javascript
test("Shallow/mocked approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = shallow(<Calendar showFilters={false} title="Choose Filter" />);

  // Act
  wrapper
    .find("filtersPanel")
    .instance()
    .showFilters();
  // Tap into the internals, bypass the UI and invoke a method. White-box approach

  // Assert
  expect(wrapper.find("Filter").props()).toEqual({ title: "Choose Filter" });
  // what if we change the prop name or don't pass anything relevant?
});
```

</details>

<br/>

## ⚪ ️ 3.4 不要 sleep，善用框架內建對非同步事件的支援，並試著加速他

:white_check_mark: **建議：** 在許多情況下，被測試單元的完成時間是未知的 (例如，因為動畫而延遲了元件的出現) — 在這種情況下，不要 sleep (例如使用 setTimeout)，而是使用大多數框架提供的更靠譜的方法。一些函示庫允許等待操作 (例如 [Cypress .request('url')](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting))，另一些函示庫提供用於等待的 API，如 [@testing-library/dom 的方法 wait(expect(element))](https://testing-library.com/docs/guide-disappearance)。有時後，更優雅的方法是 stub 那些比較慢的資源，像是 API，然後一旦響應時間變得確定，組件就可以顯式地重新渲染。當依賴一些 sleep 的外部組件時，[加快時鐘的速度](https://jestjs.io/docs/en/timer-mocks)或許能提供幫助。 sleep 是一種需要避免的模式，因為它會導致你的測試變得緩慢或有風險(如果等待的時間太短)。當 sleep 和輪詢不可避免且測試框架原生不支持時，一些 npm 的函示庫 (如 [wait-for-expect](https://www.npmjs.com/package/wait-for-expect)) 可以幫助解決半確定性問題。

<br/>

❌ **否則：** 當 sleep 的時間太長時，測試速度會慢上一個數量級。當嘗試縮短 sleep 時間時，如果被測試的單元沒有及時響應，測試將會失敗。這時你不得不在脆弱的測試和糟糕的性能之間進行權衡。

<br/>

<details><summary>✏ <b>程式範例</b></summary>

<br/>

### :clap: 正例： E2E API 在非同步的處理完後 resolves (Cypress)

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")
![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: 正例：測試的函示庫等待 DOM 元素

```javascript
// @testing-library/dom
test("movie title appears", async () => {
  // element is initially not present...

  // wait for appearance
  await wait(() => {
    expect(getByText("the lion king")).toBeInTheDocument();
  });

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

### :thumbsdown: 反例： 自製的 sleep 程式

```javascript
test("movie title appears", async () => {
  // element is initially not present...

  // custom wait logic (caution: simplistic, no timeout)
  const interval = setInterval(() => {
    const found = getByText("the lion king");
    if (found) {
      clearInterval(interval);
      expect(getByText("the lion king")).toBeInTheDocument();
    }
  }, 100);

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

</details>

<br/>

## ⚪ ️ 3.5 Watch how the content is served over the network

![](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Examples with Lighthouse")

✅ **Do:** Apply some active monitor that ensures the page load under real network is optimized - this includes any UX concern like slow page load or un-minified bundle. The inspection tools market is no short: basic tools like [pingdom](https://www.pingdom.com/), AWS CloudWatch, [gcp StackDriver](https://cloud.google.com/monitoring/uptime-checks/) can be easily configured to watch whether the server is alive and response under a reasonable SLA. This only scratches the surface of what might get wrong, hence it's preferable to opt for tools that specialize in frontend (e.g. [lighthouse](https://developers.google.com/web/tools/lighthouse/), [pagespeed](https://developers.google.com/speed/pagespeed/insights/)) and perform richer analysis. The focus should be on symptoms, metrics that directly affect the UX, like page load time, [meaningful paint](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint), [time until the page gets interactive (TTI)](https://calibreapp.com/blog/time-to-interactive/). On top of that, one may also watch for technical causes like ensuring the content is compressed, time to the first byte, optimize images, ensuring reasonable DOM size, SSL and many others. It's advisable to have these rich monitors both during development, as part of the CI and most important - 24x7 over the production's servers/CDN

<br/>

❌ **Otherwise:** It must be disappointing to realize that after such great care for crafting a UI, 100% functional tests passing and sophisticated bundling - the UX is horrible and slow due to CDN misconfiguration

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

### :clap: Doing It Right Example: Lighthouse page load inspection report

![](/assets/lighthouse2.png "Lighthouse page load inspection report")

</details>

<br/>

## ⚪ ️ 3.6 Stub flaky and slow resources like backend APIs

:white_check_mark: **Do:** When coding your mainstream tests (not E2E tests), avoid involving any resource that is beyond your responsibility and control like backend API and use stubs instead (i.e. test double). Practically, instead of real network calls to APIs, use some test double library (like [Sinon](https://sinonjs.org/), [Test doubles](https://www.npmjs.com/package/testdouble), etc) for stubbing the API response. The main benefit is preventing flakiness - testing or staging APIs by definition are not highly stable and from time to time will fail your tests although YOUR component behaves just fine (production env was not meant for testing and it usually throttles requests). Doing this will allow simulating various API behavior that should drive your component behavior as when no data was found or the case when API throws an error. Last but not least, network calls will greatly slow down the tests

<br/>

❌ **Otherwise:** The average test runs no longer than few ms, a typical API call last 100ms>, this makes each test ~20x slower

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Stubbing or intercepting API calls

![](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Examples with React") ![](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "Examples with react-testing-library")

```javascript
// unit under test
export default function ProductsList() {
  const [products, setProducts] = useState(false);

  const fetchProducts = async () => {
    const products = await axios.get("api/products");
    setProducts(products);
  };

  useEffect(() => {
    fetchProducts();
  }, []);

  return products ? <div>{products}</div> : <div data-test-id="no-products-message">No products</div>;
}

// test
test("When no products exist, show the appropriate message", () => {
  // Arrange
  nock("api")
    .get(`/products`)
    .reply(404);

  // Act
  const { getByTestId } = render(<ProductsList />);

  // Assert
  expect(getByTestId("no-products-message")).toBeTruthy();
});
```

</details>

<br/>

## ⚪ ️ 3.7 Have very few end-to-end tests that spans the whole system

:white_check_mark: **Do:** Although E2E (end-to-end) usually means UI-only testing with a real browser (See [bullet 3.6](https://github.com/goldbergyoni/javascript-testing-best-practices#-%EF%B8%8F-36-stub-flaky-and-slow-resources-like-backend-apis)), for other they mean tests that stretch the entire system including the real backend. The latter type of tests is highly valuable as they cover integration bugs between frontend and backend that might happen due to a wrong understanding of the exchange schema. They are also an efficient method to discover backend-to-backend integration issues (e.g. Microservice A sends the wrong message to Microservice B) and even to detect deployment failures - there are no backend frameworks for E2E testing that are as friendly and mature as UI frameworks like [Cypress](https://www.cypress.io/) and [Puppeteer](https://github.com/GoogleChrome/puppeteer). The downside of such tests is the high cost of configuring an environment with so many components, and mostly their brittleness - given 50 microservices, even if one fails then the entire E2E just failed. For that reason, we should use this technique sparingly and probably have 1-10 of those and no more. That said, even a small number of E2E tests are likely to catch the type of issues they are targeted for - deployment & integration faults. It's advisable to run those over a production-like staging environment

<br/>

❌ **Otherwise:** UI might invest much in testing its functionality only to realizes very late that the backend returned payload (the data schema the UI has to work with) is very different than expected

<br/>

## ⚪ ️ 3.8 Speed-up E2E tests by reusing login credentials

:white_check_mark: **Do:** In E2E tests that involve a real backend and rely on a valid user token for API calls, it doesn't payoff to isolate the test to a level where a user is created and logged-in in every request. Instead, login only once before the tests execution start (i.e. before-all hook), save the token in some local storage and reuse it across requests. This seem to violate one of the core testing principle - keep the test autonomous without resources coupling. While this is a valid worry, in E2E tests performance is a key concern and creating 1-3 API requests before starting each individual tests might lead to horrible execution time. Reusing credentials doesn't mean the tests have to act on the same user records - if relying on user records (e.g. test user payments history) than make sure to generate those records as part of the test and avoid sharing their existence with other tests. Also remember that the backend can be faked - if your tests are focused on the frontend it might be better to isolate it and stub the backend API (see [bullet 3.6](https://github.com/goldbergyoni/javascript-testing-best-practices#-%EF%B8%8F-36-stub-flaky-and-slow-resources-like-backend-apis)).

<br/>

❌ **Otherwise:** Given 200 test cases and assuming login=100ms = 20 seconds only for logging-in again and again

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Logging-in before-all and not before-each

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
let authenticationToken;

// happens before ALL tests run
before(() => {
  cy.request('POST', 'http://localhost:3000/login', {
    username: Cypress.env('username'),
    password: Cypress.env('password'),
  })
  .its('body')
  .then((responseFromLogin) => {
    authenticationToken = responseFromLogin.token;
  })
})

// happens before EACH test
beforeEach(setUser => () {
  cy.visit('/home', {
    onBeforeLoad (win) {
      win.localStorage.setItem('token', JSON.stringify(authenticationToken))
    },
  })
})

```

</details>

<br/>

## ⚪ ️ 3.9 Have one E2E smoke test that just travels across the site map

:white_check_mark: **Do:** For production monitoring and development-time sanity check, run a single E2E test that visits all/most of the site pages and ensures no one breaks. This type of test brings a great return on investment as it's very easy to write and maintain, but it can detect any kind of failure including functional, network and deployment issues. Other styles of smoke and sanity checking are not as reliable and exhaustive - some ops teams just ping the home page (production) or developers who run many integration tests which don't discover packaging and browser issues. Goes without saying that the smoke test doesn't replace functional tests rather just aim to serve as a quick smoke detector

<br/>

❌ **Otherwise:** Everything might seem perfect, all tests pass, production health-check is also positive but the Payment component had some packaging issue and only the /Payment route is not rendering

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Smoke travelling across all pages

![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
it("When doing smoke testing over all page, should load them all successfully", () => {
  // exemplified using Cypress but can be implemented easily
  // using any E2E suite
  cy.visit("https://mysite.com/home");
  cy.contains("Home");
  cy.contains("https://mysite.com/Login");
  cy.contains("Login");
  cy.contains("https://mysite.com/About");
  cy.contains("About");
});
```

</details>

<br/>

## ⚪ ️ 3.10 Expose the tests as a live collaborative document

:white_check_mark: **Do:** Besides increasing app reliability, tests bring another attractive opportunity to the table - serve as live app documentation. Since tests inherently speak at a less-technical and product/UX language, using the right tools they can serve as a communication artifact that greatly aligns all the peers - developers and their customers. For example, some frameworks allow expressing the flow and expectations (i.e. tests plan) using a human-readable language so any stakeholder, including product managers, can read, approve and collaborate on the tests which just became the live requirements document. This technique is also being referred to as 'acceptance test' as it allows the customer to define his acceptance criteria in plain language. This is [BDD (behavior-driven testing)](https://en.wikipedia.org/wiki/Behavior-driven_development) at its purest form. One of the popular frameworks that enable this is [Cucumber which has a JavaScript flavor](https://github.com/cucumber/cucumber-js), see example below. Another similar yet different opportunity, [StoryBook](https://storybook.js.org/), allows exposing UI components as a graphic catalog where one can walk through the various states of each component (e.g. render a grid w/o filters, render that grid with multiple rows or with none, etc), see how it looks like, and how to trigger that state - this can appeal also to product folks but mostly serves as live doc for developers who consume those components.

❌ **Otherwise:** After investing top resources on testing, it's just a pity not to leverage this investment and win great value

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Describing tests in human-language using cucumber-js

![](https://img.shields.io/badge/🔨%20Example%20using%20Cucumber-blue.svg "Examples using Cucumber")

```javascript
// this is how one can describe tests using cucumber: plain language that allows anyone to understand and collaborate

Feature: Twitter new tweet

  I want to tweet something in Twitter

  @focus
  Scenario: Tweeting from the home page
    Given I open Twitter home
    Given I click on "New tweet" button
    Given I type "Hello followers!" in the textbox
    Given I click on "Submit" button
    Then I see message "Tweet saved"

```

### :clap: Doing It Right Example: Visualizing our components, their various states and inputs using Storybook

![](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "Using StoryBook")

![alt text](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪ ️ 3.11 Detect visual issues with automated tools

:white_check_mark: **Do:** Setup automated tools to capture UI screenshots when changes are presented and detect visual issues like content overlapping or breaking. This ensures that not only the right data is prepared but also the user can conveniently see it. This technique is not widely adopted, our testing mindset leans toward functional tests but it's the visuals what the user experience and with so many device types it's very easy to overlook some nasty UI bug. Some free tools can provide the basics - generate and save screenshots for the inspection of human eyes. While this approach might be sufficient for small apps, it's flawed as any other manual testing that demands human labor anytime something changes. On the other hand, it's quite challenging to detect UI issues automatically due to the lack of clear definition - this is where the field of 'Visual Regression' chime in and solve this puzzle by comparing old UI with the latest changes and detect differences. Some OSS/free tools can provide some of this functionality (e.g. [wraith](https://github.com/BBC-News/wraith), [PhantomCSS](<[https://github.com/HuddleEng/PhantomCSS](https://github.com/HuddleEng/PhantomCSS)>) but might charge significant setup time. The commercial line of tools (e.g. [Applitools](https://applitools.com/), [Percy.io](https://percy.io/)) takes is a step further by smoothing the installation and packing advanced features like management UI, alerting, smart capturing by eliminating 'visual noise' (e.g. ads, animations) and even root cause analysis of the DOM/CSS changes that led to the issue

<br/>

❌ **Otherwise:** How good is a content page that display great content (100% tests passed), loads instantly but half of the content area is hidden?

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: A typical visual regression - right content that is served badly

![alt text](assets/amazon-visual-regression.jpeg "Amazon page breaks")

<br/>

### :clap: Doing It Right Example: Configuring wraith to capture and compare UI snapshots

![](https://img.shields.io/badge/🔨%20Example%20using%20Wraith-blue.svg "Using Wraith")

```
​# Add as many domains as necessary. Key will act as a label​

domains:
  english: "http://www.mysite.com"​

​# Type screen widths below, here are a couple of examples​

screen_widths:

  - 600​
  - 768​
  - 1024​
  - 1280​

​# Type page URL paths below, here are a couple of examples​
paths:
  about:
    path: /about
    selector: '.about'​
  subscribe:
      selector: '.subscribe'​
    path: /subscribe
```

### :clap: Doing It Right Example: Using Applitools to get snapshot comparison and other advanced features

![](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg "Using Applitools") ![](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Using Cypress to illustrate the idea")

```javascript
import * as todoPage from "../page-objects/todo-page";

describe("visual validation", () => {
  before(() => todoPage.navigate());
  beforeEach(() => cy.eyesOpen({ appName: "TAU TodoMVC" }));
  afterEach(() => cy.eyesClose());

  it("should look good", () => {
    cy.eyesCheckWindow("empty todo list");
    todoPage.addTodo("Clean room");
    todoPage.addTodo("Learn javascript");
    cy.eyesCheckWindow("two todos");
    todoPage.toggleTodo(0);
    cy.eyesCheckWindow("mark as completed");
  });
});
```

</details>

<br/><br/>

# Section 4️⃣: Measuring Test Effectiveness

<br/><br/>

## ⚪ ️ 4.1 Get enough coverage for being confident, ~80% seems to be the lucky number

:white_check_mark: **Do:** The purpose of testing is to get enough confidence for moving fast, obviously the more code is tested the more confident the team can be. Coverage is a measure of how many code lines (and branches, statements, etc) are being reached by the tests. So how much is enough? 10–30% is obviously too low to get any sense about the build correctness, on the other side 100% is very expensive and might shift your focus from the critical paths to the exotic corners of the code. The long answer is that it depends on many factors like the type of application — if you’re building the next generation of Airbus A380 than 100% is a must, for a cartoon pictures website 50% might be too much. Although most of the testing enthusiasts claim that the right coverage threshold is contextual, most of them also mention the number 80% as a thumb of a rule ([Fowler: “in the upper 80s or 90s”](https://martinfowler.com/bliki/TestCoverage.html)) that presumably should satisfy most of the applications.

Implementation tips: You may want to configure your continuous integration (CI) to have a coverage threshold ([Jest link](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)) and stop a build that doesn’t stand to this standard (it’s also possible to configure threshold per component, see code example below). On top of this, consider detecting build coverage decrease (when a newly committed code has less coverage) — this will push developers raising or at least preserving the amount of tested code. All that said, coverage is only one measure, a quantitative based one, that is not enough to tell the robustness of your testing. And it can also be fooled as illustrated in the next bullets

<br/>

❌ **Otherwise:** Confidence and numbers go hand in hand, without really knowing that you tested most of the system — there will also be some fear and fear will slow you down

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: A typical coverage report

![alt text](assets/bp-18-yoni-goldberg-code-coverage.png "A typical coverage report")

<br/>

### :clap: Doing It Right Example: Setting up coverage per component (using Jest)

![](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Using Jest")

![alt text](assets/bp-18-code-coverage2.jpeg "Setting up coverage per component (using Jest)")

</details>

<br/><br/>

## ⚪ ️ 4.2 Inspect coverage reports to detect untested areas and other oddities

:white_check_mark: **Do:** Some issues sneak just under the radar and are really hard to find using traditional tools. These are not really bugs but more of surprising application behavior that might have a severe impact. For example, often some code areas are never or rarely being invoked — you thought that the ‘PricingCalculator’ class is always setting the product price but it turns out it is actually never invoked although we have 10000 products in DB and many sales… Code coverage reports help you realize whether the application behaves the way you believe it does. Other than that, it can also highlight which types of code is not tested — being informed that 80% of the code is tested doesn’t tell whether the critical parts are covered. Generating reports is easy — just run your app in production or during testing with coverage tracking and then see colorful reports that highlight how frequent each code area is invoked. If you take your time to glimpse into this data — you might find some gotchas
<br/>

❌ **Otherwise:** If you don’t know which parts of your code are left un-tested, you don’t know where the issues might come from

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: What’s wrong with this coverage report?

Based on a real-world scenario where we tracked our application usage in QA and find out interesting login patterns (Hint: the amount of login failures is non-proportional, something is clearly wrong. Finally it turned out that some frontend bug keeps hitting the backend login API)

![alt text](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "What’s wrong with this coverage report?")

</details>

<br/><br/>

## ⚪ ️ 4.3 Measure logical coverage using mutation testing

:white_check_mark: **Do:** The Traditional Coverage metric often lies: It may show you 100% code coverage, but none of your functions, even not one, return the right response. How come? it simply measures over which lines of code the test visited, but it doesn’t check if the tests actually tested anything — asserted for the right response. Like someone who’s traveling for business and showing his passport stamps — this doesn’t prove any work done, only that he visited few airports and hotels.

Mutation-based testing is here to help by measuring the amount of code that was actually TESTED not just VISITED. [Stryker](https://stryker-mutator.io/) is a JavaScript library for mutation testing and the implementation is really neat:

(1) it intentionally changes the code and “plants bugs”. For example the code newOrder.price===0 becomes newOrder.price!=0. This “bugs” are called mutations

(2) it runs the tests, if all succeed then we have a problem — the tests didn’t serve their purpose of discovering bugs, the mutations are so-called survived. If the tests failed, then great, the mutations were killed.

Knowing that all or most of the mutations were killed gives much higher confidence than traditional coverage and the setup time is similar
<br/>

❌ **Otherwise:** You’ll be fooled to believe that 85% coverage means your test will detect bugs in 85% of your code

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: 100% coverage, 0% testing

![](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg "Using Stryker")

```javascript
function addNewOrder(newOrder) {
  logger.log(`Adding new order ${newOrder}`);
  DB.save(newOrder);
  Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

  return { approved: true };
}

it("Test addNewOrder, don't use such test names", () => {
  addNewOrder({ assignee: "John@mailer.com", price: 120 });
}); //Triggers 100% code coverage, but it doesn't check anything
```

<br/>

### :clap: Doing It Right Example: Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)

![alt text](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Stryker reports, a tool for mutation testing, detects and counts the amount of code that is not tested (Mutations)")

</details>

<br/><br/>

## ⚪ ️4.4 Preventing test code issues with Test linters

:white_check_mark: **Do:** A set of ESLint plugins were built specifically for inspecting the tests code patterns and discover issues. For example, [eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha) will warn when a test is written at the global level (not a son of a describe() statement) or when tests are [skipped](https://mochajs.org/#inclusive-tests) which might lead to a false belief that all tests are passing. Similarly, [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest) can, for example, warn when a test has no assertions at all (not checking anything)

<br/>

❌ **Otherwise:** Seeing 90% code coverage and 100% green tests will make your face wear a big smile only until you realize that many tests aren’t asserting for anything and many test suites were just skipped. Hopefully, you didn’t deploy anything based on this false observation

<br/>
<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: A test case full of errors, luckily all are caught by Linters

```javascript
describe("Too short description", () => {
  const userToken = userService.getDefaultToken() // *error:no-setup-in-describe, use hooks (sparingly) instead
  it("Some description", () => {});//* error: valid-test-description. Must include the word "Should" + at least 5 words
});

it.skip("Test name", () => {// *error:no-skipped-tests, error:error:no-global-tests. Put tests only under describe or suite
  expect("somevalue"); // error:no-assert
});

it("Test name", () => {*//error:no-identical-title. Assign unique titles to tests
});
```

</details>

<br/><br/>

# Section 5️⃣: CI and Other Quality Measures

<br/><br/>

## ⚪ ️ 5.1 Enrich your linters and abort builds that have linting issues

:white_check_mark: **Do:** Linters are a free lunch, with 5 min setup you get for free an auto-pilot guarding your code and catching significant issue as you type. Gone are the days where linting was about cosmetics (no semi-colons!). Nowadays, Linters can catch severe issues like errors that are not thrown correctly and losing information. On top of your basic set of rules (like [ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard) or [Airbnb style](https://www.npmjs.com/package/eslint-config-airbnb)), consider including some specializing Linters like [eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect) that can discover tests without assertions, [eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme) can discover promises with no resolve (your code will never continue), [eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme) which can discover eager regex expressions that might get used for DOS attacks, and [eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) is capable of alarming when the code uses utility library methods that are part of the V8 core methods like Lodash.\_map(…)
<br/>

❌ **Otherwise:** Consider a rainy day where your production keeps crashing but the logs don’t display the error stack trace. What happened? Your code mistakenly threw a non-error object and the stack trace was lost, a good reason for banging your head against a brick wall. A 5 min linter setup could detect this TYPO and save your day

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :thumbsdown: Anti-Pattern Example: The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug

![alt text](assets/bp-21-yoni-goldberg-eslint.jpeg "The wrong Error object is thrown mistakenly, no stack-trace will appear for this error. Luckily, ESLint catches the next production bug")

</details>

<br/><br/>

## ⚪ ️ 5.2 Shorten the feedback loop with local developer-CI

:white_check_mark: **Do:** Using a CI with shiny quality inspections like testing, linting, vulnerabilities check, etc? Help developers run this pipeline also locally to solicit instant feedback and shorten the [feedback loop](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/). Why? an efficient testing process constitutes many and iterative loops: (1) try-outs -> (2) feedback -> (3) refactor. The faster the feedback is, the more improvement iterations a developer can perform per-module and perfect the results. On the flip, when the feedback is late to come fewer improvement iterations could be packed into a single day, the team might already move forward to another topic/task/module and might not be up for refining that module.

Practically, some CI vendors (Example: [CircleCI local CLI](https://circleci.com/docs/2.0/local-cli/)) allow running the pipeline locally. Some commercial tools like [wallaby provide highly-valuable & testing insights](https://wallabyjs.com/) as a developer prototype (no affiliation). Alternatively, you may just add npm script to package.json that runs all the quality commands (e.g. test, lint, vulnerabilities) — use tools like [concurrently](https://www.npmjs.com/package/concurrently) for parallelization and non-zero exit code if one of the tools failed. Now the developer should just invoke one command — e.g. ‘npm run quality’ — to get instant feedback. Consider also aborting a commit if the quality check failed using a githook ([husky can help](https://github.com/typicode/husky))
<br/>

❌ **Otherwise:** When the quality results arrive the day after the code, testing doesn’t become a fluent part of development rather an after the fact formal artifact

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: npm scripts that perform code quality inspection, all are run in parallel on demand or when a developer is trying to push new code

```javascript
"scripts": {
    "inspect:sanity-testing": "mocha **/**--test.js --grep \"sanity\"",
    "inspect:lint": "eslint .",
    "inspect:vulnerabilities": "npm audit",
    "inspect:license": "license-checker --failOn GPLv2",
    "inspect:complexity": "plato .",

    "inspect:all": "concurrently -c \"bgBlue.bold,bgMagenta.bold,yellow\" \"npm:inspect:quick-testing\" \"npm:inspect:lint\" \"npm:inspect:vulnerabilities\" \"npm:inspect:license\""
  },
  "husky": {
    "hooks": {
      "precommit": "npm run inspect:all",
      "prepush": "npm run inspect:all"
    }
}

```

</details>

<br/><br/>

## ⚪ ️5.3 Perform e2e testing over a true production-mirror

:white_check_mark: **Do:** End to end (e2e) testing are the main challenge of every CI pipeline — creating an identical ephemeral production mirror on the fly with all the related cloud services can be tedious and expensive. Finding the best compromise is your game: [Docker-compose](https://serverless.com/) allows crafting isolated dockerized environment with identical containers using a single plain text file but the backing technology (e.g. networking, deployment model) is different from real-world productions. You may combine it with [‘AWS Local’](https://github.com/localstack/localstack) to work with a stub of the real AWS services. If you went [serverless](https://serverless.com/) multiple frameworks like serverless and [AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) allows the local invocation of FaaS code.

The huge Kubernetes ecosystem is yet to formalize a standard convenient tool for local and CI-mirroring though many new tools are launched frequently. One approach is running a ‘minimized-Kubernetes’ using tools like [Minikube](https://kubernetes.io/docs/setup/minikube/) and [MicroK8s](https://microk8s.io/) which resemble the real thing only come with less overhead. Another approach is testing over a remote ‘real-Kubernetes’, some CI providers (e.g. [Codefresh](https://codefresh.io/)) has native integration with Kubernetes environment and make it easy to run the CI pipeline over the real thing, others allow custom scripting against a remote Kubernetes.
<br/>

❌ **Otherwise:** Using different technologies for production and testing demands maintaining two deployment models and keeps the developers and the ops team separated

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: a CI pipeline that generates Kubernetes cluster on the fly <a href="https://container-solutions.com/dynamic-environments-kubernetes/" data-href="https://container-solutions.com/dynamic-environments-kubernetes/" class="markup--anchor markup--p-anchor" rel="noopener nofollow" target="_blank">([Credit: Dynamic-environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/))</a>

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪ ️5.4 Parallelize test execution

:white_check_mark: **Do:** When done right, testing is your 24/7 friend providing almost instant feedback. In practice, executing 500 CPU-bounded unit test on a single thread can take too long. Luckily, modern test runners and CI platforms (like [Jest](https://github.com/facebook/jest), [AVA](https://github.com/avajs/ava) and [Mocha extensions](https://github.com/yandex/mocha-parallel-tests)) can parallelize the test into multiple processes and achieve significant improvement in feedback time. Some CI vendors do also parallelize tests across containers (!) which shortens the feedback loop even further. Whether locally over multiple processes, or over some cloud CLI using multiple machines — parallelizing demand keeping the tests autonomous as each might run on different processes

❌ **Otherwise:** Getting test results 1 hour long after pushing new code, as you already code the next features, is a great recipe for making testing less relevant

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example: Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization ([Credit: JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4))

![alt text](assets/bp-24-yonigoldberg-jest-parallel.png "Mocha parallel & Jest easily outrun the traditional Mocha thanks to testing parallelization (Credit: JavaScript Test-Runners Benchmark)")

</details>

<br/><br/>

## ⚪ ️5.5 Stay away from legal issues using license and plagiarism check

:white_check_mark: **Do:** Licensing and plagiarism issues are probably not your main concern right now, but why not tick this box as well in 10 minutes? A bunch of npm packages like [license check](https://www.npmjs.com/package/license-checker) and [plagiarism check](https://www.npmjs.com/package/plagiarism-checker) (commercial with free plan) can be easily baked into your CI pipeline and inspect for sorrows like dependencies with restrictive licenses or code that was copy-pasted from Stack Overflow and apparently violates some copyrights

❌ **Otherwise:** Unintentionally, developers might use packages with inappropriate licenses or copy paste commercial code and run into legal issues

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Doing It Right Example:

```javascript
//install license-checker in your CI environment or also locally
npm install -g license-checker

//ask it to scan all licenses and fail with exit code other than 0 if it found unauthorized license. The CI system should catch this failure and stop the build
license-checker --summary --failOn BSD

```

<br/>

![alt text](assets/bp-25-nodejs-licsense.png)

</details>

<br/><br/>

## ⚪ ️5.6 Constantly inspect for vulnerable dependencies

:white_check_mark: **Do:** Even the most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community tools such as [npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit), or commercial tools like [snyk](https://snyk.io/) (offer also a free community version). Both can be invoked from your CI on every build

❌ **Otherwise:** Keeping your code clean from vulnerabilities without dedicated tools will require to constantly follow online publications about new threats. Quite tedious

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: NPM Audit result

![alt text](assets/bp-26-npm-audit-snyk.png "NPM Audit result")

</details>

<br/><br/>

## ⚪ ️5.7 Automate dependency updates

:white_check_mark: **Do:** Yarn and npm latest introduction of package-lock.json introduced a serious challenge (the road to hell is paved with good intentions) — by default now, packages are no longer getting updates. Even a team running many fresh deployments with ‘npm install’ & ‘npm update’ won’t get any new updates. This leads to subpar dependent packages versions at best or to vulnerable code at worst. Teams now rely on developers goodwill and memory to manually update the package.json or use tools [like ncu](https://www.npmjs.com/package/npm-check-updates) manually. A more reliable way could be to automate the process of getting the most reliable dependency versions, though there are no silver bullet solutions yet there are two possible automation roads:

(1) CI can fail builds that have obsolete dependencies — using tools like [‘npm outdated’](https://docs.npmjs.com/cli/outdated) or ‘npm-check-updates (ncu)’ . Doing so will enforce developers to update dependencies.

(2) Use commercial tools that scan the code and automatically send pull requests with updated dependencies. One interesting question remaining is what should be the dependency update policy — updating on every patch generates too many overhead, updating right when a major is released might point to an unstable version (many packages found vulnerable on the very first days after being released, [see the](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/) eslint-scope incident).

An efficient update policy may allow some ‘vesting period’ — let the code lag behind the @latest for some time and versions before considering the local copy as obsolete (e.g. local version is 1.3.1 and repository version is 1.3.8)
<br/>

❌ **Otherwise:** Your production will run packages that have been explicitly tagged by their author as risky

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: [ncu](https://www.npmjs.com/package/npm-check-updates) can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions

![alt text](assets/bp-27-yoni-goldberg-npm.png "ncu can be used manually or within a CI pipeline to detect to which extent the code lag behind the latest versions")

</details>

<br/><br/>

## ⚪ ️ 5.8 Other, non-Node related, CI tips

:white_check_mark: **Do:** This post is focused on testing advice that is related to, or at least can be exemplified with Node JS. This bullet, however, groups few non-Node related tips that are well-known

 <ol class="postList"><li name="e3e4" id="e3e4" class="graf graf--li graf-after--p">Use a declarative syntax. This is the only option for most vendors but older versions of Jenkins allows using code or UI</li><li name="1fdc" id="1fdc" class="graf graf--li graf-after--li">Opt for a vendor that has native Docker support</li><li name="edcd" id="edcd" class="graf graf--li graf-after--li">Fail early, run your fastest tests first. Create a ‘Smoke testing’ step/milestone that groups multiple fast inspections (e.g. linting, unit tests) and provide snappy feedback to the code committer</li><li name="0375" id="0375" class="graf graf--li graf-after--li">Make it easy to skim-through all build artifacts including test reports, coverage reports, mutation reports, logs, etc</li><li name="df82" id="df82" class="graf graf--li graf-after--li">Create multiple pipelines/jobs for each event, reuse steps between them. For example, configure a job for feature branch commits and a different one for master PR. Let each reuse logic using shared steps (most vendors provide some mechanism for code reuse)</li><li name="19b0" id="19b0" class="graf graf--li graf-after--li">Never embed secrets in a job declaration, grab them from a secret store or from the job’s configuration</li><li name="b70d" id="b70d" class="graf graf--li graf-after--li">Explicitly bump version in a release build or at least ensure the developer did so</li><li name="957c" id="957c" class="graf graf--li graf-after--li">Build only once and perform all the inspections over the single build artifact (e.g. Docker image)</li><li name="339b" id="339b" class="graf graf--li graf-after--li">Test in an ephemeral environment that doesn’t drift state between builds. Caching node_modules might be the only exception</li></ol>
<br/>

❌ **Otherwise:** You‘ll miss years of wisdom

<br/><br/>

## ⚪ ️ 5.9 Build matrix: Run the same CI steps using multiple Node versions

:white_check_mark: **Do:** Quality checking is about serendipity, the more ground you cover the luckier you get in detecting issues early. When developing reusable packages or running a multi-customer production with various configuration and Node versions, the CI must run the pipeline of tests over all the permutations of configurations. For example, assuming we use MySQL for some customers and Postgres for others — some CI vendors support a feature called ‘Matrix’ which allow running the suit of testing against all permutations of MySQL, Postgres and multiple Node version like 8, 9 and 10. This is done using configuration only without any additional effort (assuming you have testing or any other quality checks). Other CIs who doesn’t support Matrix might have extensions or tweaks to allow that
<br/>

❌ **Otherwise:** So after doing all that hard work of writing testing are we going to let bugs sneak in only because of configuration issues?

<br/>

<details><summary>✏ <b>Code Examples</b></summary>

<br/>

### :clap: Example: Using Travis (CI vendor) build definition to run the same test over multiple Node versions

<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# Team

## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg"/>
<br/>

**Role:** Writer

**About:** I'm an independent consultant who works with Fortune 500 companies and garage startups on polishing their JS & Node.js applications. More than any other topic I'm fascinated by and aims to master the art of testing. I'm also the author of [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

**📗 Online Course:** Liked this guide and wish to take your testing skills to the extreme? Consider visiting my comprehensive course [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com)

<br/>

**Follow:**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 Contact](https://testjavascript.com/contact-2/)
- [✉️ Newsletter](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**Role:** Tech reviewer and advisor

Took care to revise, improve, lint and polish all the texts

**About:** full-stack web engineer, Node.js & GraphQL enthusiast

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**Role:** Concept, design and great advice

**About:** A savvy frontend developer, CSS expert and emojis freak

## [Kyle Martin](https://github.com/js-kyle)

**Role:** Helps keep this project running, and reviews security related practices

**About:** Loves working on Node.js projects and web application security.

## Contributors ✨

Thanks goes to these wonderful people who have contributed to this repository!

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://geospatialscott.blogspot.com/"><img src="https://avatars3.githubusercontent.com/u/1326248?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Scott Davis</b></sub></a><br /><a href="#content-stdavis" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AdrienRedon"><img src="https://avatars2.githubusercontent.com/u/5978436?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Adrien REDON</b></sub></a><br /><a href="#content-AdrienRedon" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/NoriSte"><img src="https://avatars0.githubusercontent.com/u/173663?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Stefano Magni</b></sub></a><br /><a href="#content-NoriSte" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.joer.im"><img src="https://avatars2.githubusercontent.com/u/47742486?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yeoh Joer</b></sub></a><br /><a href="#content-yjoer" title="Content">🖋</a></td>
    <td align="center"><a href="http://jhonnymoreira.dev"><img src="https://avatars0.githubusercontent.com/u/2177742?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jhonny Moreira</b></sub></a><br /><a href="#content-jhonnymoreira" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Germanika"><img src="https://avatars2.githubusercontent.com/u/8846678?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ian Germann</b></sub></a><br /><a href="#content-Germanika" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/AbdelrahmanHafez"><img src="https://avatars3.githubusercontent.com/u/19984935?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Hafez</b></sub></a><br /><a href="#content-AbdelrahmanHafez" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://www.ruxandrafediuc.com"><img src="https://avatars1.githubusercontent.com/u/11021586?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ruxandra Fediuc</b></sub></a><br /><a href="#content-ruxandrafed" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jacklee814"><img src="https://avatars0.githubusercontent.com/u/9951291?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jack</b></sub></a><br /><a href="#content-jacklee814" title="Content">🖋</a></td>
    <td align="center"><a href="https://www.petercarrero.com"><img src="https://avatars0.githubusercontent.com/u/231727?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Peter Carrero</b></sub></a><br /><a href="#content-aloyr" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/huhgawz"><img src="https://avatars3.githubusercontent.com/u/369338?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Huhgawz</b></sub></a><br /><a href="#content-huhgawz" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/haakonmb"><img src="https://avatars1.githubusercontent.com/u/7099302?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Haakon Borch</b></sub></a><br /><a href="#content-haakonmb" title="Content">🖋</a></td>
    <td align="center"><a href="https://jaimemendoza.com/"><img src="https://avatars3.githubusercontent.com/u/5395811?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jaime Mendoza</b></sub></a><br /><a href="#content-jaimemendozadev" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/camerondunford"><img src="https://avatars0.githubusercontent.com/u/840612?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Cameron Dunford</b></sub></a><br /><a href="#content-camerondunford" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/shadowspawn"><img src="https://avatars1.githubusercontent.com/u/15719847?v=4?s=100" width="100px;" alt=""/><br /><sub><b>John Gee</b></sub></a><br /><a href="#content-shadowspawn" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/aurelijusrozenas"><img src="https://avatars0.githubusercontent.com/u/3273544?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Aurelijus Rožėnas</b></sub></a><br /><a href="#content-aurelijusrozenas" title="Content">🖋</a></td>
    <td align="center"><a href="http://aaronshivers.com"><img src="https://avatars2.githubusercontent.com/u/42848750?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Aaron</b></sub></a><br /><a href="#content-aaronshivers" title="Content">🖋</a></td>
    <td align="center"><a href="https://tomdoes.tech/"><img src="https://avatars1.githubusercontent.com/u/8683577?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Tom Nagle</b></sub></a><br /><a href="#content-tomanagle" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/yvesyao"><img src="https://avatars0.githubusercontent.com/u/7723729?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yves yao</b></sub></a><br /><a href="#content-yvesyao" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/Userbit"><img src="https://avatars1.githubusercontent.com/u/34487074?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Userbit</b></sub></a><br /><a href="#content-Userbit" title="Content">🖋</a></td>
    <td align="center"><a href="https://glaucialemos.netlify.com/"><img src="https://avatars0.githubusercontent.com/u/1631477?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Glaucia Lemos</b></sub></a><br /><a href="#maintenance-glaucia86" title="Maintenance">🚧</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://twitter.com/koooge"><img src="https://avatars2.githubusercontent.com/u/7419215?v=4?s=100" width="100px;" alt=""/><br /><sub><b>koooge</b></sub></a><br /><a href="#content-koooge" title="Content">🖋</a></td>
    <td align="center"><a href="https://twitter.com/michalbiesiada"><img src="https://avatars0.githubusercontent.com/u/18367606?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Michal</b></sub></a><br /><a href="#content-mbiesiad" title="Content">🖋</a></td>
    <td align="center"><a href="http://roywalker.me"><img src="https://avatars0.githubusercontent.com/u/611846?v=4?s=100" width="100px;" alt=""/><br /><sub><b>roywalker</b></sub></a><br /><a href="#content-roywalker" title="Content">🖋</a></td>
    <td align="center"><a href="https://dangen-effy.github.io/"><img src="https://avatars3.githubusercontent.com/u/23185799?v=4?s=100" width="100px;" alt=""/><br /><sub><b>dangen</b></sub></a><br /><a href="#content-dangen-effy" title="Content">🖋</a></td>
    <td align="center"><a href="https://dev.to/mbiesiad"><img src="https://avatars1.githubusercontent.com/u/60202305?v=4?s=100" width="100px;" alt=""/><br /><sub><b>biesiadamich</b></sub></a><br /><a href="#content-biesiadamich" title="Content">🖋</a></td>
    <td align="center"><a href="https://tarojsx.github.io"><img src="https://avatars3.githubusercontent.com/u/127009?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yanlin Jiang</b></sub></a><br /><a href="#content-cncolder" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/sanguino"><img src="https://avatars2.githubusercontent.com/u/2077168?v=4?s=100" width="100px;" alt=""/><br /><sub><b>sanguino</b></sub></a><br /><a href="#content-sanguino" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/MorganGeek"><img src="https://avatars0.githubusercontent.com/u/3721240?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Morgan</b></sub></a><br /><a href="#content-MorganGeek" title="Content">🖋</a></td>
    <td align="center"><a href="https://luk4s.dev"><img src="https://avatars0.githubusercontent.com/u/8350985?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Lukas Bischof</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=lukasbischof" title="Tests">⚠️</a> <a href="#content-lukasbischof" title="Content">🖋</a></td>
    <td align="center"><a href="https://juanmaruiz.surge.sh"><img src="https://avatars2.githubusercontent.com/u/1837650?v=4?s=100" width="100px;" alt=""/><br /><sub><b>JuanMa Ruiz</b></sub></a><br /><a href="#content-JuanMaRuiz" title="Content">🖋</a></td>
    <td align="center"><a href="https://luisangelorjr.com.br"><img src="https://avatars3.githubusercontent.com/u/22268900?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Luís Ângelo Rodrigues Jr.</b></sub></a><br /><a href="#content-luisangelorjr" title="Content">🖋</a></td>
    <td align="center"><a href="https://jfernandezpe.wordpress.com/"><img src="https://avatars0.githubusercontent.com/u/12046620?v=4?s=100" width="100px;" alt=""/><br /><sub><b>José Fernández</b></sub></a><br /><a href="#content-jfernandezpe" title="Content">🖋</a></td>
    <td align="center"><a href="http://www.linkedin.com/in/AlejandroGutierrezB"><img src="https://avatars3.githubusercontent.com/u/56408597?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alejandro Gutierrez Barcenilla</b></sub></a><br /><a href="#content-AlejandroGutierrezB" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/jasonandmonte"><img src="https://avatars1.githubusercontent.com/u/30088000?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Jason</b></sub></a><br /><a href="#content-jasonandmonte" title="Content">🖋</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/otavionetoca"><img src="https://avatars.githubusercontent.com/u/11263232?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Otavio Araujo</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=otavionetoca" title="Tests">⚠️</a> <a href="#content-otavionetoca" title="Content">🖋</a></td>
    <td align="center"><a href="https://contributor.pw"><img src="https://avatars.githubusercontent.com/u/5027939?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Alex Ivanov</b></sub></a><br /><a href="#content-contributorpw" title="Content">🖋</a></td>
    <td align="center"><a href="https://github.com/YeeJone"><img src="https://avatars.githubusercontent.com/u/20400822?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Yiqiao Xu</b></sub></a><br /><a href="#content-YeeJone" title="Content">🖋</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->
