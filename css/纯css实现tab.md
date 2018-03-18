# 纯CSS实现tab栏（可切换）

```css
    .tabs {
        height: 271px;
    }

    .tab {
        float: left;
    }

    .tab-radio {
        display: none;
    }

    .tab-header {
        color: #fff;
        background-color: #FF6D00;
        display: block;
        border-radius: 5px 5px 0 0;
        padding: 10px 16px 10px 16px;
        margin-right: 4px;
        border-bottom: 1px #FF6D00 solid;
        font-weight: 600;
    }

    .tab-radio:checked + .tab-header {
        background-color: #fff;
        border: 1px solid #b9b9b9;
        z-index: 99;
        position: relative;
        border-bottom: 1px #fff solid;
    }

    .tab-content {
        position: absolute;
        width: 496px;
        height: 230px;
        left: 0;
        display: none;
        border: #b9b9b9 solid 1px;
        border-radius: 0 8px 8px;
        top: 42px;
        font-size: 150px;
        line-height: 230px;
        text-align: center;
        color: white;
    }

    .tab-radio:checked + .tab-header + .tab-content {
        display: block;
    }

    .tab-radio:checked + .tab-header-1 {
        background-color: #D50000;
        border-bottom: 1px #D50000 solid;
    }

    .tab-radio:checked + .tab-header + .tab-content-1 {
        background-color: #D50000;
    }

    .tab-radio:checked + .tab-header-2 {
        background-color: #304FFE;
        border-bottom: 1px #304FFE solid;
    }

    .tab-radio:checked + .tab-header + .tab-content-2 {
        background-color: #304FFE;
    }

    .tab-radio:checked + .tab-header-3 {
        background-color: #00C853;
        border-bottom: 1px #00C853 solid;
    }

    .tab-radio:checked + .tab-header + .tab-content-3 {
        background-color: #00C853;
    }
```

```html
<div class="tabs">
    <div class="tab">
        <input type="radio" name="tab-radio" class="tab-radio" id="tab-radio-1" checked>
        <label for="tab-radio-1" class="tab-header tab-header-1">TAB-1</label>
        <div class="tab-content tab-content-1">
            TAB-1
        </div>
    </div>
    <div class="tab">
        <input type="radio" name="tab-radio" class="tab-radio" id="tab-radio-2">
        <label for="tab-radio-2" class="tab-header tab-header-2">TAB-2</label>
        <div class="tab-content tab-content-2">
            TAB-2
        </div>
    </div>
    <div class="tab">
        <input type="radio" name="tab-radio" class="tab-radio" id="tab-radio-3">
        <label for="tab-radio-3" class="tab-header tab-header-3">TAB-3</label>
        <div class="tab-content tab-content-3">
            TAB-3
        </div>
    </div>
</div>
```