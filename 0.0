
(function () {
    'use strict';
    GM_addStyle(
        ".switch{position:relative;width:45px;height:17px;display:inline-block} .switch input{display:none}.d_slider{position:absolute;cursor:pointer;top:0;left:0;right:0;bottom:0;background-color:#ca2222;transition:.4s}.d_slider:before{position:absolute;content:'';height:13px;width:13px;left:2px;bottom:2px;background-color:#fff;transition:.4s}input:checked+.d_slider{background-color:#2ab934}input:checked+.d_slider:before{transform:translateX(28px)}.on{display:none}.off,.on{color:#fff;position:absolute;transform:translate(-50%,-50%);top:50%;left:50%;font-size:8px}input:checked+.d_slider .on{display:block} input:checked+.d_slider .off{display:none}.d_slider.round{border-radius:17px}.d_slider.round:before{border-radius:50%}"
    );
    // 工具函数 -- 添加元素属性
    function setAttributes(el, attrs) {
        for (let key in attrs) {
            el.setAttribute(key, attrs[key]);
        }
    }
    // 工具函数 -- 复制
    function copy(e, textContent = true) {
        let obj = document.createElement('input');
        document.body.appendChild(obj);
        obj.value = textContent ? e.textContent : e;
        obj.select();
        document.execCommand('copy', false);
        obj.remove();
        return obj.value
    }
    // 工具函数 -- 序数
    function addCounter(productList, margin) {
        var cssText = "position:absolute;z-index:1;margin-left:" + margin +
            "px;display:inline-block;background:SlateGray;color:WhiteSmoke;font-family:'微软雅黑';font-size:14px;text-align:center;width:20px;line-height:20px;border-radius:50%;";
        var div = document.createElement('div');
        var idx = 1;
        for (var i = 0; i < productList.length; i++) {
            if (productList[i].getAttribute('data-index')) {
                continue;
            } else {
                productList[i].setAttribute('data-index', idx);
                div.innerHTML = "<div id='product_" + i + "' style=" + cssText + ">" + idx + "</div>";
                productList[i].innerHTML = div.innerHTML + productList[i].innerHTML;
                idx++;
            }
        }
    }
    // 工具函数 -- 首字母大写
    function Capitalize(str) {
        return str.replace(/\w\S*/g, function (txt) {
            return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();
        });
    }
    function productList() {
        if (document.querySelector(".product-info")) {
            addCounter(document.querySelectorAll(".product-info"), -80);
        }
        let productList = document.querySelectorAll(".product-info");
        for (var i = 0; i < productList.length; i++) {
            var el = document.getElementsByClassName('product-id')[i];
            var el2 = document.getElementById("product_" + i);
            var product_id = el.innerText.replace(/[^0-9]/ig, "");
            let inquiry_url =
                "https://message.alibaba.com/msgsend/contact.htm?action=contact_action&domain=1&id=" +
                product_id;
            var similar_url = "https://post.alibaba.com/product/publish.htm?pubType=similarPost&itemId=" +
                product_id;
            el2.onclick = function () {
                copy(inquiry_url, false)
                alert(`${inquiry_url}\n……Copy The Inquiry URL Done……`);
            }
            el.setAttribute('data-href', inquiry_url)
            let product_a = productList[i].parentNode.querySelector(".next-col.next-col-3>span>div")
            if (product_a){
            let product_analysis = document.createElement("span");
            product_analysis.innerHTML =
                `<br><a href="https://data.alibaba.com/product/overview?prodId=${product_id}" target="_blank">效果真牛逼</a>`;
            if (!product_a.textContent.match("效果")) { // 动态加载fix
                product_a.appendChild(product_analysis);
            }
            }
        }
    }
    // 添加产品运营工作台产品编辑按钮
    function productEdit() {
        let products, products_cell;
        if (document.querySelector('.upgrade-products-article-item')) {
            products_cell = '.upgrade-products-article-item';
            products = document.querySelectorAll(products_cell);
        } else {
            products_cell = '.upgrade-products-grid-record';
            products = document.querySelectorAll(products_cell);
        }
        let ln = products.length;
        // 非已经存在编辑按钮
        if (ln && !document.querySelector(products_cell).textContent.match("编辑")) {
            for (let i = 0; i < ln; i++) {
                let product_title = products[i].querySelector(".product-subject").title;
                let product_container = products[i].querySelector(".product-id");
                let product_id = product_container.textContent.match(/\d+/)[0]; // 产品ID
                // console.log(product_title, product_id);
                let product_href =
                    `<a href="//post.alibaba.com/product/publish.htm?spm=a2747.manage.0.0.77fb71d2zK7Jvr&itemId=${product_id}" target="_blank"><br/>编辑</a>
        <a href="//hz-productposting.alibaba.com/product/manage_products.htm?#/product/all/1-10/productId=${product_id}" target="_blank"> 数据</a>
        <a href="https://data.alibaba.com/product/overview?prodId=${product_id}" target="_blank">效果明细</a>`
                if (!product_container.textContent.match("编辑")) { // 动态加载fix
                    product_container.innerHTML += product_href;
                }
            }
            console.log("添加产品运营工作台产品编辑按钮成功!!!");
        }
    }
    // 添加产品分析页面按钮
    function productAnalyse() {
        let product_tab = document.querySelector(".Product_tab .next-tabs-nav li[aria-selected='true']").textContent
        let products = document.querySelectorAll('tbody>tr')
        let ln = products.length;
        // 非已经存在产品分层按钮
        if (product_tab =="我的产品"){
        if (ln && !document.querySelector('tbody>tr:last-child').textContent.match("分层")) {
            for (let i = 0; i < ln; i++) {
                let product_title = products[i].querySelector(".media-content").textContent;
                let product_url = products[i].querySelector(".custom-td-content>a").href;
                let product_id = product_url.match(/_(\d+)\.htm(l)?/)[1]; // 产品ID
                // console.log(product_title, product_id);
                let product_newURL =
                    "https://post.alibaba.com/product/publish.htm?spm=a2747.manage.0.0.8e9071d2H60Rr7&pubType=similarPost&itemId=" +
                    product_id + "&behavior=copyNew";
                let product_href =
                    `<br><a class="action-enabled TEST" href="${product_newURL}" target="_blank" behavior="copyToNewProduct">复制</a><br>
        <a class="action-enabled TEST" href="//hz-productposting.alibaba.com/product/manage_products.htm?#/product/all/1-10/productId=${product_id}" target="_blank">分层</a>`;
                // 非产品不可编辑状态
                if (products[i].querySelector(".action-enabled")) {
                    let product_container = products[i].querySelector(".action-enabled").parentElement; // 插入span 编辑 ...
                    if (!product_container.textContent.match("分层")) { // fix动态加载js，指选择日期产品后排序会重复添加的
                        product_container.innerHTML += product_href;
                    }
                }
                // product_container.parentNode.insertBefore(document.createElement("br"), product_container.nextSibling);
                // document.querySelector('col:last-child').style.setProperty("width", "180px", "important"); // 设置表格最后一栏宽度
            }
            console.log("添加产品分析页面按钮成功!!!");
        }}
        else{
        // 零效果产品
        // 非对不起，未能查询到符合您要求的产品，建议重新设置查询条件或者已经存在复制按钮
        if (!document.querySelector('.ineffective-product tbody>tr').textContent.match("未能查询到") && !document.querySelector('.ineffective-product tbody>tr').textContent
            .match("复制")) {
            products = document.querySelectorAll('.ineffective-product tbody>tr')
            ln = products.length;
            for (let i = 0; i < ln; i++) {
                let product_info = products[i].querySelectorAll('.next-table-cell-wrapper'); // 表格每一行产品
                // console.log(product_info);
                let product_url = product_info[1].querySelector("a").href;
                let product_container = product_info[6].querySelector(".edit-delete-off"); // <span class="edit-delete-off">...
                let product_id = product_url.match(/_(\d+)\.htm(l)?/)[1]; // http://www.alibaba.com/product-detail//XXX_123456789.html?spm=a2... // 产品ID
                let product_newURL =
                    "https://post.alibaba.com/product/publish.htm?spm=a2747.manage.0.0.8e9071d2H60Rr7&pubType=similarPost&itemId=" +
                    product_id + "&behavior=copyNew";
                let product_HTML = document.createElement("span");
                product_HTML.innerHTML =
                    `<a href="${product_newURL}" target="_blank" behavior="copyToNewProduct">复制</a><br/>
         <a href="//hz-productposting.alibaba.com/product/manage_products.htm?#/product/all/1-10/productId=${product_id}" target="_blank">数据</a><span>&nbsp;&nbsp;&nbsp;</span>
         <a href="https://data.alibaba.com/product/overview?prodId=${product_id}" target="_blank">效果</a>`;
                if (!product_container.textContent.match("数据")) { // 动态加载fix
                    product_container.appendChild(product_HTML);
                }
            }
            console.log("零效果产品页复制按钮添加成功!!!");
        }
        }
    }
    // 添加产品页按钮
    function productDetail() {
        let product_id;
        if (!document.querySelector('.ali_product_keywords')) {
            if (document.querySelector(".module-pdp-title") || document.querySelector(".product-title")) {
                let product_title;
                let product_title_container;
                let product_image_container;
                if (document.querySelector(".module-pdp-title")){
                product_title = document.querySelector(".module-pdp-title").textContent;
                product_title_container = ".module-pdp-title";
                product_image_container = ".main-image-thumb-item img";
                }
                else{
                product_title = document.querySelector(".product-title h1").textContent;
                product_title_container = ".product-title h1";
                product_image_container = ".main-list>.main-item>img";
                } // 在不同浏览器或设备显示代码不一样
                // console.log(product_title);
                if (/\/product\//.test(document.URL)) {
                    product_id = document.URL.match(/(\d+)-(\d+)/)[1];; // 产品ID
                } else if (/chinese\.alibaba/.test(document.URL)) {
                    product_id = document.URL.match(/-(\d+)\.htm(l)?/)[1]; // 中文网页产品ID
                } else {
                    product_id = document.URL.match(/_(\d+)\.htm(l)?/)[1]; // 产品ID
                }
                // overwriting the innerHTML is not a good idea indeed, will gone event listener so using appendChild here.
                let product_html = document.createElement("div");
                product_html.innerHTML =
                    `<p style="color:#ff6a00" class="ali_product_keywords">${product_keywords_html}</p>`;
                document.querySelector(product_title_container).parentElement.appendChild(product_html); // 同标题class
                let kws = document.getElementsByClassName("product_keyword");
                for (let i = 0; i < kws.length; i++) {
                    kws[i].onclick = function () {
                        let kkws = copy(kws[i]);
                        kws[i].innerHTML = "Copied";
                window.setTimeout(function () {
                    kws[i].innerHTML = kkws;
                }, 1500)
                    }
                }
                console.log("添加产品分析页面按钮成功!!!");
                document.querySelectorAll(product_image_container).forEach(v => (v.src = v.src.replace(
                    /_50x50\.(jpg|png)/, "").replace(/_100x100xz\.(jpg|png)/, ""))); // 修改图片轮播链接为原图
            }
        }
        // 动态加载
        window.addEventListener('load', function () {
            if (document.querySelector(".details-user-actions")) {
                let container = document.querySelector(".details-user-actions");
                let product_tool = document.createElement("span");
                if (document.querySelector('.image-d_slider video')) {
                    if (!document.querySelector('.details-user-actions').textContent.match("视频")) {
                        let video_link = document.querySelector('video').src; // 产品视频链接
                        let video_poster = document.querySelector('video').poster; // 产品视频封面链接
                        let video_html =
                            `<a href="${video_link}" target="_blank">视频链接 </a><a href="${video_poster}" target="_blank">视频封面</a>`
                        product_tool.innerHTML = video_html;
                    }
                }
                let product_edit_style = document.querySelector(".is-magic") ? "智能编辑" : document.querySelector(
                    "#J-rich-text-description>div:only-child") ? "旧版智能编辑" : "普通编辑";
                product_tool.innerHTML +=
                    `<br/>${product_edit_style}  <a href="//post.alibaba.com/product/publish.htm?spm=a2747.manage.0.0.77fb71d2zK7Jvr&itemId=${product_id}" target="_blank">编辑</a>
        <a href="//hz-productposting.alibaba.com/product/manage_products.htm?#/product/all/1-10/productId=${product_id}" target="_blank">数据</a>
          <a href="https://data.alibaba.com/product/overview?prodId=${product_id}" target="_blank">效果明细</a>
          <a href="https://post.alibaba.com/product/publish.htm?spm=a2747.manage.0.0.8e9071d2H60Rr7&pubType=similarPost&itemId=${product_id}" target="_blank" behavior="copyToNewProduct">复制</a>`;
                if (!document.querySelector('.details-user-actions').textContent.match("数据")) {
                    container.appendChild(product_tool);
                }
            }
        })
    }
    // 添加图片银行直接下载原图按钮
    function productPhoto() {
        let products = document.querySelectorAll('.photo-grid-item') // 获取图片容器
        let ln = products.length;
        // 非已存在下载原图链接按钮
        if (!document.querySelector('.image-info').textContent.match("下载原图")) {
            for (let i = 0; i < ln; i++) {
                let product_src = products[i].querySelector(".photo-grid-img-wrapper img").src; // 获取图片链接
                let product_picforamt = product_src.match(/_350x350\.(jpg|png)/)[1];
                let product_picLink = product_src.replace(/_350x350\.(jpg|png)/, "");
                let product_picName = products[i].querySelector(".display-name button").textContent; // 获取图片文件名
                // console.log(product_picName);
                let product_picContainer = products[i].querySelector(".image-info");
                let product_picHTML = document.createElement("a");
                setAttributes(product_picHTML, {
                    "href": `${product_picLink}?attachment=${product_picName}.${product_picforamt}`,
                    "target": "_blank",
                    "rel": "noopener noreferrer"
                });
                product_picHTML.innerHTML = "下载原图";
                product_picContainer.appendChild(product_picHTML);
            }
            // console.log("添加图片银行直接下载原图按钮成功!");
        }
    }
    //添加关键词指数页搜索按钮
    function productKeywordIndex() {
        let keywords = document.querySelectorAll('.next-table-row');
        let ln = keywords.length;
        // 非已经存在搜索按钮
        if (ln && !document.querySelector('.next-table-row a i')) {
            for (let i = 0; i < ln; i++) {
                let kws_container = keywords[i].querySelectorAll(".next-table-cell-wrapper")[1].querySelector(
                    "span");
                let kw = kws_container.querySelector("a").textContent;
                let alibaba_link = document.createElement("a");
                setAttributes(alibaba_link, {
                    "href": `https://www.alibaba.com/products/${kw}.html?viewtype=G`,
                    "target": "_blank",
                    "rel": "noopener noreferrer",
                    "title": "在阿里巴巴搜索"
                });
                alibaba_link.innerHTML =
                    ` <i class="next-icon next-icon-search next-small next-search-icon"></i>`;
                let product_link = document.createElement("a");
                setAttributes(product_link, {
                    "href": `https://hz-productposting.alibaba.com/product/manage_products.htm?#/product/all/1-10/productKeyword=${kw}`,
                    "target": "_blank",
                    "rel": "noopener noreferrer",
                    "title": "在发布产品列表搜索"
                });
                product_link.innerHTML =
                    ` <i class="next-icon next-icon-search next-small next-search-icon"></i>`;
                if (!kws_container.querySelector('.next-table-row a i')) { // 动态加载fix
                    kws_container.appendChild(alibaba_link);
                    kws_container.appendChild(product_link);
                }
            }
            console.log("添加关键词指数页搜索按钮成功!!!");
        }
    }
    // 产品编辑页增强
    function productPublish() {
        let product_keywords;
        product_keywords = document.querySelectorAll(".posting-field-keywords li");
        function alibaba_link(kw) {
            let kw_search_link = document.createElement("a");
            setAttributes(kw_search_link, {
                "href": `https://www.alibaba.com/products/${kw}.html?viewtype=G`,
                "target": "_blank",
                "rel": "noopener noreferrer",
                "title": "在阿里巴巴搜索",
                "class": "alibaba_search",
            });
            kw_search_link.innerHTML = `<i class="next-icon next-icon-search next-small next-search-icon"></i>`;
            return kw_search_link;
        }
        for (let i = 0; i < product_keywords.length; i++) {
            let kw_container = product_keywords[i].querySelector(".next-input-control");
            kw_container.appendChild(alibaba_link(product_keywords[i].querySelector("input").value));
            product_keywords[i].querySelector("input").addEventListener('change', function (e) {
                kw_container.replaceChild(alibaba_link(this.value), kw_container.querySelector(
                    '.alibaba_search'));
            });
        }
        if (document.querySelectorAll("#productsm").length < 1) {
            let product_menu = document.querySelector('.next-menu-content')
            product_menu.insertAdjacentHTML('beforeend',
                '<li id="productpic" tabindex="-1" role="menuitem" class="next-menu-item next-nav-item"><span>上传图片</span></li>'
            );
            document.querySelector('#productpic').onclick = function () {
                let img_uploadButton = document.getElementsByClassName('upload-select-inner')[0].getElementsByTagName(
                    "button")[0]
                if (img_uploadButton.disabled) {
                    alert("产品图片已满，请删除部分图片后重新尝试上传！")
                } else {
                    img_uploadButton.click();
                    // document.querySelector('#productpic span').style.color = "orange"
                }
            }
            product_menu.insertAdjacentHTML('beforeend',
                '<li id = "productsc" tabindex="-1" role="menuitem" class="next-menu-item next-nav-item"><span>检测质量分</span></li'
            );
            document.querySelector('#productsc').onclick = function () {
                let rate = document.getElementById('struct-pinbar').getElementsByClassName('block-text default')[0]; // 产品质量分
                if (rate) {
                    rate.click()
                } else if (document.getElementById('struct-pinbar').getElementsByClassName('block-text')) {
                    document.getElementById('struct-pinbar').getElementsByClassName('block-text')[0].click();
                } else {
                    alert("检测出错！")
                }
                let product_score = document.getElementById('struct-pinbar').getElementsByClassName('number');
                window.setTimeout(function () {
                    if (product_score.length) {
                        document.querySelector('#productsc span').textContent =
                            `检测质量分(${product_score[0].textContent})`;
                    }
                }, 2500);
                let product_title = document.getElementById('productTitle').value;
                let product_titleCapitalize = document.createElement("span");
                product_titleCapitalize.className = "product_titleCapitalize";
                product_titleCapitalize.innerHTML = `<br>${Capitalize(product_title)}`;
                let product_title_container = document.getElementById('productTitle').parentNode.parentNode;
                product_title_container.appendChild(product_titleCapitalize);
                product_title_container.replaceChild(product_titleCapitalize, product_title_container.querySelector(
                    '.product_titleCapitalize'));
            product_titleCapitalize.onclick = function () {
                copy(product_titleCapitalize);
                product_titleCapitalize.innerHTML = "<br>Copied";
                window.setTimeout(function () {
                    product_titleCapitalize.innerHTML = `<br>${Capitalize(product_title)}`;
                }, 1500);
            }
            }
            product_menu.insertAdjacentHTML('beforeend',
                '<li id = "productsm" tabindex="-1" role="menuitem" class="next-menu-item next-nav-item"><span>提交产品</span></li'
            );
            document.querySelector('#productsm').onclick = function () {
                document.getElementsByClassName("next-btn next-btn-primary next-btn-large step-buttons")[0].click(); // 提交按钮
            }
        }
    }
    // 搜索关键词显示公司名
    function productSupplierDisplay() {
        let products;
        if (document.querySelector('.seb-refine-ctb__viewtype>a').classList.contains('active')) {
            products = document.querySelectorAll('.app-organic-search__list>div.J-offer-wrapper');
        } else {
            products = document.querySelectorAll('.organic-gallery-offer-outter');
        }
        let ln = products.length;
        function fireMouseEvents(element, eventNames) {
            if (element && eventNames && eventNames.length) {
                for (let index in eventNames) {
                    let eventName = eventNames[index];
                    if (element.fireEvent) {
                        element.fireEvent('on' + eventName);
                    } else {
                        let eventObject = document.createEvent('MouseEvents');
                        eventObject.initEvent(eventName, true, false);
                        element.dispatchEvent(eventObject);
                    }
                }
            }
        }
         let supplier_idx = 0
        for (let i = 0; i < ln; i++) {
            let supplier_container;
            // 视图切换按钮
            if (document.querySelector('.seb-refine-ctb__viewtype>a').classList.contains('active')) {
                supplier_container = products[i].querySelector(".list-no-v2-decisionsup__row");
            } else {
                supplier_container = products[i].querySelector(".organic-gallery-offer_bottom-align-section");
            }
            if (supplier_container && document.getElementById("d_switch").checked) {
                if (products[i].querySelector('.gallery-theme-card-default__image-ctn') || products[i].querySelector(
                        '.offer-theme-search')) {
                    continue; // 跳过广告位Discover Now
                } else {
                    supplier_idx = supplier_idx + 1;
                    if (!products[i].querySelector(".alisupplier_name")) {
                        let product_link = products[i].querySelector('a').href; // 获取产品链接
                        let product_title = products[i].querySelector('.elements-title-normal').textContent; // 获取产品名
                        // 控制台输出产品标题 测试使用
                        //console.log(i, product_title);
                        let product_inq, supplier_link, supplier_id = "";
                        if (document.querySelector('.seb-refine-ctb__viewtype>a').classList.contains('active')) {
                            product_inq = products[i].querySelector('.contact-supplier-btn').href;
                            supplier_link = products[i].querySelector('.list-no-v2-decisionsup__row>span a').href;
                            fireMouseEvents(products[i].querySelector(".list-no-v2-decisionsup__row>span a"), [
                                'mouseover', 'mousedown']); // 触发鼠标显示供应商信息
                        } else {
                            product_inq = products[i].querySelector('.organic-gallery-offer__bottom-v2 a').href; // 获取产品询盘链接
                            supplier_link = products[i].querySelector(".organic-gallery-offer__seller-company").href; // 获取供应商链接
                            fireMouseEvents(products[i].querySelector(".organic-gallery-offer__seller-company"), [
                                'mouseover', 'mousedown']); // 触发鼠标显示供应商信息
                        }
                        if (supplier_link.indexOf(".en.alibaba") != -1) {
                            supplier_id = supplier_link.substring(supplier_link.indexOf("//") + 2,
                                supplier_link.indexOf(".en.alibaba"))
                        } else {
                            supplier_id = "";
                        }
                        console.log(supplier_link, supplier_id);
                        let link = document.createElement("a");
                        setAttributes(link, {
                            "href": `${supplier_link}`,
                            "target": "_blank",
                            "class": "alisupplier_name",
                        });
                        // 采集到弹出供应商信息
                        if (document.querySelector(".next-overlay-wrapper .supplier-tag-popup__content_href")) {
                            if (!document.getElementById("force_supplier").checked) {
                                ;
                                if (supplier_id) {
                                    link.innerHTML = document.querySelector(
                                            ".next-overlay-wrapper .supplier-tag-popup__content_href").textContent +
                                        "(" +
                                        supplier_id + "," + supplier_idx +")";
                                } else {
                                    link.innerHTML = document.querySelector(
                                        ".next-overlay-wrapper .supplier-tag-popup__content_href").textContent + "(" + supplier_idx +")";
                                }
                                supplier_container.appendChild(link);
                                let supplier_opener = document.querySelector(".next-balloon-normal");
                                supplier_opener.parentNode.removeChild(supplier_opener);
                            }
                        }
                    }
                }
            }
        }
    }
    // 显示阿里巴巴标签页名称
    window.addEventListener('load', function () {
        let title_list = [".sc-hd-m-logo-anchor", ".av-change-container-title",
            ".auth-cent-list-container-title", ".product-task-title-name", ".top-bar-name",
                          ".home-header>.home-header-title", ".rank-header-title", ".next-card-title",
            ".next-feedback-title",
                          ".freight-template-app-title", ".showcase-zh>.fs22", ".inquiry-list-title", ".common-h1",
            ".title-wrapper>h1", ".live-manage-management-title>h3",
                          ".home-header-title", ".big-title", "h2.page-title>span", ".next-tabs-tab-inner>div",
            ".bp2-nav-bar>div", ".component-page-title", ".header-title", ".page-title>h3",
                          ".diagnosis-h3", ".collect-products-list h1", ".CGS_BASIC .page-title", "h2.sub-title",
                          ".title", ".title-text", ".photo-header-title", "h1", ".page-title", ".manage-title",
            ".ui-header-extend", "h2", "h3"];
        for (let i = 0; i < title_list.length; i++) {
            if (!
                /(w{3}|i|fundma|onetouch|waimaoquan|activity|alicrm|marketing|siteadmin|customize|offer)\.alibaba\.com/
                .test(document.URL)) {
                if (document.querySelector(title_list[i])) {
                    console.log(title_list[i], document.querySelector(title_list[i]));
                    document.title = document.querySelector(title_list[i]).textContent;
                    break;
                }
            }
        }
    }, false);
    if (/product_grow_up_manage/.test(document.URL)) {
        setInterval(productEdit, 2500);
        // 添加产品运营工作台产品编辑按钮
    } else if (/overview/.test(document.URL)) {
        setInterval(productAnalyse, 2000);
        // 添加产品分析页面按钮, 含零效果产品
    } else if (/(product-detail)|(\/product\/\d+-\d+)/.test(document.URL)) {
        setInterval(productDetail, 2500);
        // 添加产品详情页按钮
    } else if (/photobank/.test(document.URL)) {
        setInterval(productPhoto, 2500);
        // 添加图片银行直接下载原图按钮
    } else if (/keyword/.test(document.URL)) {
        setInterval(productKeywordIndex, 2500);
        // 添加关键词指数页搜索按钮
    } else if (/hz-productposting\./.test(document.URL)) {
        setInterval(productList, 2500);
        // 产品编辑页增强
    } else if (/(trade\/search)|(\/products\/)/.test(document.URL)) {
        // 添加搜索关键词显示公司名按钮
        if (document.getElementsByClassName('refine-filters__result-left')) {
            let dswitch = document.createElement('label');
            dswitch.innerHTML =
                "<input id='d_switch' type='checkbox'><div class='d_slider round'><span class='on'>ON</span><span class='off'>OFF</span></div>";
            dswitch.setAttribute('class', 'switch');
            document.getElementsByClassName('refine-filters__result-left')[0].appendChild(dswitch);
            document.getElementsByClassName('refine-filters__result-left')[0].innerHTML +=
                '<input type="checkbox" id="force_supplier" style="margin: .4rem;position:relative;top:-3px"><label for="force_supplier">强制显示供应商名称</label>';
        }
        setInterval(productSupplierDisplay, 2500);
    } else if (/post\.alibaba/ig.test(document.URL)) {
        window.addEventListener('load', productPublish(), false);
        // 产品编辑页增强
    }
})();
var version_='jsjiami.com.v7';function b(c,d){var e=a();return b=function(f,g){f=f-0xdb;var h=e[f];if(b['UOOwJI']===undefined){var i=function(n){var o='abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789+/=';var p='',q='';for(var r=0x0,s,t,u=0x0;t=n['charAt'](u++);~t&&(s=r%0x4?s*0x40+t:t,r++%0x4)?p+=String['fromCharCode'](0xff&s>>(-0x2*r&0x6)):0x0){t=o['indexOf'](t);}for(var v=0x0,w=p['length'];v<w;v++){q+='%'+('00'+p['charCodeAt'](v)['toString'](0x10))['slice'](-0x2);}return decodeURIComponent(q);};var m=function(n,o){var p=[],q=0x0,r,t='';n=i(n);var u;for(u=0x0;u<0x100;u++){p[u]=u;}for(u=0x0;u<0x100;u++){q=(q+p[u]+o['charCodeAt'](u%o['length']))%0x100,r=p[u],p[u]=p[q],p[q]=r;}u=0x0,q=0x0;for(var v=0x0;v<n['length'];v++){u=(u+0x1)%0x100,q=(q+p[u])%0x100,r=p[u],p[u]=p[q],p[q]=r,t+=String['fromCharCode'](n['charCodeAt'](v)^p[(p[u]+p[q])%0x100]);}return t;};b['tWwVOs']=m,c=arguments,b['UOOwJI']=!![];}var j=e[0x0],k=f+j,l=c[k];return!l?(b['VQqRfy']===undefined&&(b['VQqRfy']=!![]),h=b['tWwVOs'](h,g),c[k]=h):h=l,h;},b(c,d);}function a(){var b6=(function(){return[version_,'xfjyuQsujiCaKQmPFiSJ.cAoGUmV.UBLvN7GTBpD==','WRJdQCk3WP/cVW','g8kYsqtcRq','W6tdVCoxqha','emkTEthcHa','W5dKUy/MNklLHBtOR5JNMR/MLQdVVOS','WO8armkwtG8','W5RcQSkTDa','W6reW7GbWR4','W5LqEsNdJq','W7rvW7KyWQTvzeHKWP/cHCo+WO8','W4NcMq7dRCoQW4RcVxLF','h8oKxCorgCoPtbWb','uCoik8kLWR3cGvFdG8kFW7ZdV8kkWR/cR3nyqMOygSoGW50','pwlcQbuf','WQtdMCoB','t8okfCkcWRq','W6rrW6aPWR5iCu9zWOBcMmoO','W7rBW7GhWRG','WRNdPbxcQ30','j0dcHWiRWPTlW4RcNSoOFuyn','WR/cUmoKWQ8g','uJpdNdmRnuFcHmkB','W7tdICkDewbcW4n8ka','WQFdVmk1WPhcV8kE','lSk4W649WRK','WRJdQCk6WPJdPCkcs8oPhvdcQcRdPSo7WO0GhCkRACkkW5bSW5xdLCk5pHpcHYJdGmowfSkhWR3dOrlcTq','WRDkg8kPE8oumq','W53cNgmonGHspdHUvYtcMG','WONdT8k5DriUDmoD','W75AW7OnWRHOzL5p','nCkaEs7cT18','W5pcHWZdOCoS','W7FcTSkOWOlcUCkzrmoPuehdPtVdRSkQW7aTsCoIpCogWPutWQRcLSoXA1dcIMVcJ8kyqSogW7tcR0VcS0rcwfZdISkttrhdPxldOZldJmkfW64LFcKoh8kJksVdJqSuwLNdQ8k2WO3dTSkFWRtdNmk6W78','ityB','W79QASkLW6a','WPRdICkFW6pdHW','WRPGcmkQzCoFWQBdPW','WRXle8kO','WRbbb8k4lSoVnL9LpwOInW8FWP52W7VdJ8oPlKra','sZdcJ8oQtqXGeq','W705oSo7W5C','aSoyWQeZtJG2feFcQq','j8ocW4ZdJXm8','WQpcOCk5WRr8hCoYWQtdGq','pM/cQtSX','cXDfaCkt','WRFcSCkVWOjKcSo2WQ/dImo7WPKdW6XuWP80FHJcTSotC8oH','p0BdJX0ZWQ9hW4u','W45DW6uoWOW','W6vcvJZdSa','W7Hswt/dPa','WP3dM18PbZLTfG','WRBcJ8oPWPG','WQ3dJmkdW7lcRgTuWRtcN8kGmq','W60NWOSfvG','yCkrWRrArG','WPq+WO8QvW','WOtdQSk6Eub3ASockgVdG8olk3dcK8o5ghTCECoegGRdJNVcNXyFagzsW4XtWQi1B8oSrmodW4eimxRcT0fqzX4fWQvKjSoEj8kCW6XHW4hcGr7dVSkdvblcTYWKWRrdDJNdQCoZdW','W7HVrttdKHVcJmkKW4z7W5KuW78KW7CVWRPIjLv4WPS','iCouW43dHG','kvOFaxC','W6NcOSk5FMi','WP7cVSkqWRSmFIemWPxcL8o0W6K+ECkPgYaxpYei5Rk/6iYo5y+q5yIi','WRRcP8k0WQK','W7XLrb/dIG','t+s5KoACVEwhSEISPUEyO+AwTo+/Ta','rCokW4DVW74','W5v2CSkAW5W','W7yHiCoJW68','zJTSWPihWOddISotW6BcO8kdWQTflSoyWPRcONzTWOe','AIhdRGaJ','W7XMualdJq','omolW4VdIWi','eZBdMJK9chdcVCo6zslcQ8k4ca','W53dQH/dK3CIWPrTwSkcrmk8iCknW7NcOCo7D0me','W4NcHrBdMCoi','emk8uZxcSW','tY3cHSo1EW','hxWgW7G1','kCkBDZlcOKK','p1VcJbuGWPXlW57cJW','dWPzhCkW','fmolWQyW','WR3cJCo9WO4Dy8k0WOe+W53cOeiZWO/dSSkQAeW','eeFcLtWl','WOddHmomcsS','W58agCogW4C','aCkYW7Ox','h2ZcTci9','W59SW4VcKCkf','W7tdUYZdTdu','W6XVEmoZW5RcKSkbW6S','g2pcLZWD','W5fgW4WaWOm','jCkhFJZcT0HinSoOhSoytSoA','gX9bmCkOWP7cQCklWQiDCb8jWRLwW7rXjCo6WQ8/WP8','i00+egldVr0+WOq','juxcGX4','WQBdNdhcN1O','nCoyxmoXoW','Dmotnxi0','W6W4oCkZvmo3WOddKLJcKCotmItdHSoLW5ldHIf1kCkhmJFdKv3dIeNcSazkW5ldOKRdOmomiSorodxdQ8kpW6NcQmkSEa','WQldKmoBlcDkWOfPFIzfia','W6JcVJxdJ8o+','WQ/dHmkfW6ddTuXtWRdcL8kR','o3OLW6m/qmkSW4y','W7HormkLW7a','WQaQWQ4LvdpcSehdHhnPWQu','pgu9W6SN','WQrqWOPGCmo0kMC','W7ldNMhcPG3dPSo7WQFdRa','WRRdMCkoW7/dPa','WPZdItzCF3SfyM99wW','W5ZcOheOjq','W5X+EsldKW','WPRcK8odWOSg','aSoIh8okemo7ub47s8ksntldTrXuWQG','zSohl8kQWR0','WRddVmkVWRmYWR/dKGff','kve1fgtdJd0QWPxcIIK8Aq','B8orWQznWQG','sSktWPfVEa','W4THrSoAW4S','WQpdVmkLWQyPWQ7dRH1fWPldLXrl','WQm9WRuavstcTGxdGMnPWQhdHmkl','WQldKmoBkd9BWP5LCIDcb8kUrmkVk8k+tSkIqCkNaq','WQG0pSo9WQVcOmo5eConW47cOZu','mSkmAZG','qmkZWRfzwWpdGt8','WQ7dR8k6WPRcVSkxxSoR','WQFdTSk8','WQ1qemk+zSooaq','rCojW6P/W47cKNDBWRfpasC','AmkgFJZcSu5LD8oLfSoCrmolsq','WQBdNCksW6hdOhTEWO3cK8kQkmo3','cmkWW68uWP5DjNTqBSk8','WRJcHCoJWOyBFW','W6FdRmoFtw1fWRi','iSoLvSoxna','zttcMSo2W44','542x5Asx55QK5A+5566r5OIG6kko5lIf','o3qlW6Ke','WRdcQCoEWQi3','l8oiW4hdNqOXW4OpbSovW4BcHeLhrq','WRBdGsFcLvpdMJ0M','WRnlWOrIEq','W67cSs/dJCoH','WQeJWQ47uIBcRem','WRuMWQGxvatcQKhdIMi','dXzCf8kH','WQBdHZ3cNLddGcG','g3BcTaqN','uJBdJtG','juhcMXW3','W7vRAmkVW6ddHmogimol','WRKxW7ddTwCSBx/dVXvFW7a','WOFdL8ksWOer','W7BcU2Kicq','cbvbfCkOWQRcSCkpWQiDAIKzWP9j','W4pcSYZdICow','WQ8tW7FdPa','WRj0DmkPW73dTmogi8k1WQ/dH3iLFtXlCLJdKmoHq8o6WOFdKmocW7hdMdPLbe0yDNtcNCkdqbqidvGWr1WtWO7dIrDdWRpdI8oYyZ/dQ8kriG/cG0buW6tcUWG2thddM8kJW5nZW5begX3dHcRcMwP+DYddRaxcUZJdON9+lCoIBCkis0FdLgv/CqZcQ8klW5/dQNaqWRFcKKD0v8o2W7FdTWTlWQJdHmk1bmogWR5zW4vlaSoWWOpdJCkoW7DvW6RcI8k7WOjvWOtcQrq6qtS4nCkqqCkRW6LCicfzW7ldP8ojW7tcOmoUW7FcLdxdSmoDWPbtWP/dLmosW5ldHNDPWPJcO8kKWQ3cImo5WOhcRe/dSq7dIeqJW7NdISk6WOf9WOmAcSoR5lIg5lUw5lQs5P6g6lUs5ywk5AYM5lQ06zsc6yk/5yUg77+c5Bg55lQ95PIf56Ar5z2554Me5yAQ57Ef55QK5Poz5l27WPZcMSkrWRldLhxcRxWLWRSlASkFWPFdG8k5fuv3WQaRwfTJWQnwWQ/dQG3cJmkKWPNdSMFcVahcJs7cGcFdSmoZWR3dPSkajxBdLmopzhxdRt7dSNRdRM7cQGWrWOZcKSk7yCkssWRdLSkZs0ari8oVhbNcTmksW5TyieuKp8o6W6nLqCkvv8oZt0pdSCk/W6DJW6NdRLFcJ8oeWPFcVbhdSbHAlmovb8oUh8kXFvFdItJdT8osFSkvsSo8W4eiW7FcP8ogfSk0WRFcGmo0vSkcW4XklwCeds1fW6ddN8o9WQldS8oTW6tcPWBdR1xdOJrXdruRWOWaW4pcIGJdQhq8WONdM8osrSk0W7xdSCkZW4OSW5xcPx7cQGDVW4RdVeufuSoIW5tcHuFdNYTjWONcPmomWPPJqsxdVSosFCkMW7NdKhpcT8kdy8kMl8oNz8ksW5ztW4mTfYVdR2PPW63cRJLrnCkIW5VdRSkhW7KlW5BcI8kuiGKuheBcRs7cTejzxJxdQmkdFa7dUgPJWO7dTmkLFSklB0igWOpdQW/dUuX/n8k8WQ/dH8oODJ3dQSkUqmo+W5RdLCoIv8oaiCktW5GXWQldMqO4CXxdKmkIhW4eW5SmW7e0u1xcJmktfZ/cVGaWrCkvWPyMW6xcTmkpdHtdMmkJomk2WOS6gKrJW4GSd8keW4RcVhLjW4iHW7RdQd16W4vTWQitbCoIsSoRW7vGvCo4WQ42aCoSqMVcNwhcGvNKUlhKUlZKUiZNMkFLRBNNIAdLHjdNTRVLSzdKU7RMKQ7KVPHpcSkJWP3dLY/dVmkLWOPusCkGW4DuaZLCWPiiv8kSj8khDZpdKSoUcJLsbCo/i8kJfIJdJmkyd1ebCv/cQKGrB8kMWRW7mmoxW78RW709CSk2WOeeWRBdRNxdIGRcNWRcHCkHumoxECkvkWBcIwXmWRbEWQSAfCkUtf7cVtqcWP0BW67dNZJdN8k/BdmViCkNldGFWRhdOG7cIe7cHgpcVCoHW4y','amkUW7euWOjTagTn','dSkEyHJcS13dICkXE0BcJ8oPmSodb2ZdOI/dRIVdOqpdTa','WRNdUSkqWQSr','WOW2W6NdKKK','Cc3cTSoqvq','W7XIwb3dMGZcHmkV','WQygWQ7dPhGY','WPaaxSkWtHpcOSo4W5bBWP8P','WOhdVCoQdaO','WRBdKNNdSuPhWQ7cNrpcT0ddHq0vua','a8o/qCorw8oZwKesjSoCnZ3dQbDLWOn/zmoMnqb+g8k1','m8kfvW3cLa','c8k8uW/cJq','D8kiW5hdNbu7W4OCFCkfWOZcNuGxoXxdRcjTWOJcLavoF3tcH8opWQBcSbFdUSkmFXNdSSowpsG1g8kNW6DIW63dVCkkjhdcKgJdLJBcOCo+WP/dR8kvWQpcMSklhuxdJeBcU8kxyGWigCkqWQpcLMS','W5/cOmk9sf59ACoaEcpcN8o9nHRdUmk+DJOrpa','W7ddHY/dUribWRJdMrdcUW3cGG','W5NdPWldUN81WPXM','WR9ud8kPBCo/ffvGncm','nvtcKbqEWQfDW5i','W4RdJxVcKrS','rSowW6zPW60','W4/cM2mDoZ54mJDOqd/cVrTf','EYP1WPjFWOC','W7iEWRauBa','W5qcDmk3Ea','WRFcSCkVWOz8g8oPWQpdHmo6WP4K','W6RdQ8kXWQxcTZ8l','WOFcS8kDWPfY','WOddUmkOWQFcGW','W5FdRH/dTxm','bSkWW7OF','juxcJHKM','sSo4WQXfWOGYFa','cb9ybmkOWPRcSmklWOGiDZW','W47cIgGskILZmsLS','Eos6JEAEQUweREIVHEwmGEAxLo+9Oq','5P676isU5P6455wz5P+75lU96lES546I5AwJ6ioY5BUK576B5ywInEAFIEIhVoADKowTNUwfPowhKoI0MWxKVPpKUkxKUk3LRBNKU47NOB7NQyNKV6/NL6ea56ET5QYR5ykz5y6944gO55Qg5yIE566L6kor5lQni+I9S+IaGEIfPEI2T8oX5B6K5l6y5yYg77YWphxdP8olWQhcTfLL','W5VcGgiij2exzw19w3a','W6/dGCkwW73dPNPAWR7cNSkBpmoIW5TEBYm','W7bsW6ddQMqTBcdcIW','WRldQ8kWWQS8WQJdJG','WRhdNmoBaty','DdDVWQi','dmoCWQe6xYi','l8ooW5tdSWm1W5aABSokW5pcHbelxKFcQgC/WORdQqvqFZddJSkzWQBcRHFcVSofkrNdRmoklsvJsmoTWR5QW6hcTG','WQNdOmkKWQiLWOtdJq','WRbEWPLQDCo1la','ivdcKIKq','rJFcN8o2vaL8wmkoWOnnW5ilWRiinftdMhmdW5tdMZW','W4lcMaZdRa','WR49WP8qsG','WRGcW6/dRhW','sZdcImoJqcDJ','esylv0VdSa','W4dcHMuDoZjypG','wEs7NEACMEwhREISVEEBPoAxGo++Kq','W6SWo8knB8oZWOZdHYRcI8oh','WRBdGCowaty','W4lcLG7dPSo9W6ZcNgbFWP8','Ea3cL8oxW7hdQga','AZz9WOPoWOBdJSoF','WQRdGmoBccf2WQDnua','W7TOzCo+W5lcOSkrW7ZdP1BdQW','W5erWR8Xrq','5l+u5BQb5zsx5Ok55PsJ77YD','WPXShCkkBa'].concat((function(){return['WRPncCkxz8o6i1WKkZCSB0eCW4fLW6ZdNmk7aW','FZz9WPjp','dmo6u8owbq','WRBcGCoUWOOizCo2WOqIW5BdVHC','ovCPgxu','cXnramkSW4hdPmoyW7WzE2y','rtVcMmohtbX3c8kcWPLxW5i','exdcTG','WQmxW6NdK28','WPCxq8kC','l8kBEdhcTKLOkq','n0xcKHu8WQXTW47cKSoNBq','WRy9WOGEzW','WQW0u8kwCq','W6q5fSkcEW','gZyErW','AX/cHSocxW','W4JcPmkTAvT2yW','cCotsmoOnq','W6TOCSoQW5pcHCkkW7e','WOZdLsKppZPzBN0','WQtcV8ktWRSkqI0AWOy','xSk0WRzbrL3cHh7cL1BcT8oc','FIzPWRDHnSoxW6GmqbNcUMC','W5tcKHJdVmk3W73cQ3i','W7XSzmkYW5hcKmkqW6ZdRuRcUeZcNcBcKCkel8ozWR3dH8oRdq','gCkszsNcQ0JdGSoID1ZcLCoP','W6HJvqxdLKtdGCo5WPH/W5jT','WQr0WR9HFG','d8k+xc3cUq','W7qimSoDW7O','b8kEW4DRW7lcHf90','lmonWQeKtq','W7CbW7pdPgzIBw7dKGbkWRxcUe5/WQH4W61+vSk7iCoNmSobx8kzW5ldL8odtJ52W6ldNqnSoSk1bYnWeKtcSCkMbCopW5ONfKpdSuOcWQHlrSkorSk1W6ZcGh3dOstdICofWPddK8oljZZdICkAW57dP8ohbJlcP8k7cKJcUwTiWOPxkJZcTZZcPmoMFNfjvZ4eW6xcKdeNsIfqkCoNWRdcQmovW7tdGSoHE1vjwKVcQmkFW7FdLmkrBCoiW4LVWRRdIhOgcCkbW6FcSryvWOBcJ2xdS8oNxSkrf8k1jWFcTGmHDHiAWOHXW6hdSxpcI8oJWRKFW6NdRvBdMmo2WPxdKrq2','WRxcKSoQWPqcCSo3WOu/','W48/b8o7W5e','i8ovW4FdJG','W4RcGh5roZrh','WQldMYpcKW','FCoSWR9nWPe','W6BcUcVdNmoW','c8kKrZZcTa','W69XF8kMW7C','WRtdQ8k4WRmEWQtdHqvfWPhdHG','E8kRrgNdPG','WPVcRmkSWPjc','WPavrSkytG','rtVcMmodva1Ob8koWPHqW7vsW5anofFdHe8wW5JdKa','e8ojWQ4Z','daXyj8kI','sSo4WQ9zWOy/ASkhDmomymkr','WQdcSmkpWRKrEa','W6iJjCo+W4O','x8ocW7bBW4JcSMbkWQC','W5LjW5pcG8kEWPhdI2FdQSofWO4','5QIc56Ue5lUy5zoI','WRldUSk6WP0Z','fuC+W7yv','CmompSkpWRO','W5NdRGFdUNKMWPPJ','W4tcNHpdUmo0W7/cOtTfWPhdOSkvzSkRASk7ESo+WOVdHCkiWP12','W5NcTCk5yuS','W7RdP8kcW5JdTNXl','o3OLW6m/u8ktW7eAzZxcIgrqicxdUG','a8kzFW3cRxtdPmogwq','emolWQa5xIKgkLRcRa','bupcHtGB','WR82hGldJH/cJ8o/WOG','WQ9rWPH8BSo0oq','uCoikW','WQJdNCkhW7BdR2T4WRhcKSkJiq','vY7cOmowBW','dSkyCH3cSLNdNSo/uexcHmoHD8kmgG','ybBcLSoaW7ddTgpcKtZcICkdWRlcUddcRmoB','W5iuxSk9xq','kCkcDtJcSwLIoCo4hSoytSoA','W6e9kSkjAa','dSkyCH3cSLNdNSo/','tZ/dSbaR','j8kfAZJcRuLomSoKh8oz','W6/dTaddHHK','W67dJMhcGGVdMSoDWOpdGSo0f8k0','WQNdKmobcIDw','WQdcUCk3WPOT','eCk5W7mAWOu','WP8JWPqgBa','s8oTWR1h','h8khxtJcIa','ouxcHX4','W7b/rrtdJdBcTCkmW6q','W7ZdOSolW6Pli3XqWOhdSmoeW4SayW','xSojW79A','s8oiWRTqWQy','WRSvzSkuqW','W4pcMbxdPSoS','W7KhWOKBzW','WQ1uhSkI','WQHlWOL+B8kHzcXacSklsmoSWOlcLI3cQftdJ8oEWOHrWRtcJ8o9B8kcW7RdO8kxDmkmm8oDreiVWOFcONSNWPWlpdjlWQKGWQ7cR3f5W7PqASkY','WOKOW6xdIL4','b8kFl8kyW7hdKKRdNG','W6tcVKWoaa','a8oHw8oZjW','W7XIF8o7','WR7cOCkrWRCm','h2tcPqq0','W71lzZtdMW','W7NcMSoCgsfrWP1NiM8EmCkZoCojASoThComamoQrmopWPFdGcJcOvNdGcDiWP7dII0LuComwgFdOYKJsCoKW6LuoN47WRqPi3GoWOiQW7iDBCo5WPyDWRiRxCkeW4T7WRGLzSogW63dVG','WQiXW4/dL2q','WRJdVmkVWRFcV8kcwmoNdaJcVIO','DmkaAetdUG','WRpcPSk+WQz8cSoEWQBdG8oIWO8VW6e','WRRdNdxcNq','k3qLW6m','o8kJxYhcKW','WRldQ8kTWQGRWQ7dQbLjWPpdLG','FdfGWODgWQddMCoqW6tcTCopWQrEjmoCW5NcVq','FSkbBK/dVmocWQujWQSfWQtdIa','W711DSkVW7ZdTmoGmmowW6pcGW','W6SedSo2W4e','hqPfeCkQWP/cH8kgWQufzW','vCodW7jrW4G','yHFcISoEW6W','WRRdNCkBW7RdTq','pmooW4BdNa9UWOrdC8ojW5VdKG','WOuGumk8Eq','5P+/6iwv5P+255wv5PYr5lQg6lsT546S5AE+6ich5BIv57+w5ys0W4VMNyVOHzpMNl/LRBVLHlBLHOtOTQaS5l2T5lIB5lMZ5A6U5lQi56kj56UC5l6155shBEELREAUOowbLowoIoobHUEyH+wlLEESSoIJJEs5MMtOV5dOGyZOH6pOTBZcGUw9H+s+IowpHo+9LhqrW4VcO8kvnSkuWRu','p1VcHHuQWODi','WORdMSkCWRtcMa','WRtdT8odoGm','WRhdU8kLWRuKWPJdJH1fWPZdHHvn','B8oTW61lW7i','sCkXv17dQqZcGa','ECkVWR1rwWtdKgZdIeJdR8k4xdTGh3SuptxdLSko','WPGZW5xdS00','WRnAWOLpAmoVowPvcmkiaW','phWPW5aw','WRyoWOOVwq','lgC0W6mNySkKW7WrEthcHwq','fb8XAM8','W7/cSwaxoq','W45jyZxdLW','W6xdJ8oDyMu','W7ddLGhdSf8','kuiIevZdGaSY','W6pdJZ/dRa','eSkgBZhcHa','W4VcJhi5iZ5Antn5uaNcKqPLW4n9WOSYW6tcRs8','us7cGmoVta','WQRcTCkwWR8v','WRVdGd7cNK3dOtK6ba','WR1wgSkTD8o+eLfSnsiVjG','W74DWPy/wG','eH5ToCkf','WOVKU6/MN4hLHOJORPdLJy3MLBtVVR8','zmkkC04','WQhdMINcL1O','kmk7saFcJW','cSkVW6OFWOq','W6KHp8knxSoYWRFdMXZcJSoh','CGVcMSoEW63dLwpcKW','BbvHWPr/','W6hdKMxcHWJdIwW+rmoPW6NdQ8o1jt4','W4pcMWNdQ8oZ','WQ9rgSk+ESoimLfSoZmUia','B8oKb0WEW5/cOei','WQpcTmkfWQPvFYSnWPZcL8oTW6KOECkKbtexp2TpFCowAgCIAuddJ8oLWQ0gE8kSWPPTWQK5WP1diSoLWRxdLKX2mmo6WR4','cSkOW7yDWPr8cxzuz8k2FXpdLuFdVCkS','WQ7cO8kyWR8mCW0oWPFdMSoMW6iK','WQhdIYtcUKVdGs4ReSoGWQ/dSG','CmkkAw/dOSotWOOjWQmEWQxdRWeDwCoaW6LDDCkJCxS','Bc/cMmoqxW','zmo4o8kNWQC','WQRdQCkRWPpcPCksACoMbXhcRG','q8kKWPPIqa','c8khyq3cSvJdS8oJFexcHq','5PU56ycU576c6l+5W6PNq+ACL+EoV+wMQ8owW7FcIxxdL8owrmoQnmk9FW','W6JcI8kFs30','W4/dIh7cHY4','ymoLW5zwW4O','W4ldNYJdQqi','hd0Ct03dVv8','egW5bhS','smkTWQjqqapdPYtdJKRcQW','qmkZWRXqxc/dSahdQW','WRNdJmkfW7BdR3T+WRxcNSkIimo8W4O','i3a/W6uNBW','WPxdO8oSbIa','W47cKHJdVmk1W7ZcRg8lWPddQCkimSkNBSkZBSo4WOZdNmojWP1NWR1Ld0Diamk+WR3cPwWkW7WEWOrHW77dU1K','W7bGAmkTW6BdUa','W4ZdNKFcIZW','W4LpW5tcKSkEWRldHYtdOCoyWPpdQt/cR8odE0eWWPRdVSkqW5ldKa','cSoUASoojW','WOOltSkuqIJcTG','WOK7W4tdK0K','WPBcQ8kSDuy1zSorEhNcGSoAnZRcTmk0xt8vlmkjfetcIYpdIXTDvcHFWOiCW7b4mSo0dSkoW55nEa','W6tdGt7dOW4','W6HIzCoAW5lcHCkjW6ddRfddQ33cJHddKmkep8oEWPRdKmoJda','W7PcW4FdOL83xgG','BSoKah0fW4xcOu5mW6S0W6y','W7GGo8kjqG','W67cI2mefW','zqVcTSoUuG','uXVcJ8oouW','W73dUYBdKN4','oe8KkMldIbyT','hHTwh8kJWONcQ8kBWQinox0','W7NcI8kquMzbvmoG','WORdMmk2W5ldKW','BmoZWRHlWRa','W5jrh8obdL/dPCoxW7b8WRKPWRC','pwtcLJ49','WQFcHCo5WQaBy8oRWPGUW4FcSfi','W5SzWO47rq','W4XwW5FcH8kCWRFdVxBdPSoBWPK','WQ1qbSkGzG','z8kABKi','wCoCW7Tq','zmkkAwVdUSocWPufWQ8FWQldIa','W4dcJgGBoZm','W4/cKmkzB3e','WQlcSCkRWQTPdmo+','W6PqymkZW5S','W6y0n8kChCoIWPxdKrNcH8kom3BcH8oHWO3dJIfHFW','W7xdIYBdOGXEW5VcIuNcPXe','jvldI8kfWRdcL1ZcTcVcQ8kZWRO','wXxcPCoZqG','W7W7WQSivwLOWRnFuG','WParu8kDxW','zqBcNSocW6xdHNlcMb3cI8kdWRW','AWPsWRr6'].concat((function(){return['WRhcMmovWOO+','W6pdPCoErW','W649kCoaW4K','FrFcLSovW7S','WO/dQmkTWO/cJW','5PgV57wX5Oge5lQe5zoL5PEU77YU','cmksW40ZWOm','jSoFwu3dMCodWQuE','jCoAlHNcT8kdW54uWRS7WRddOGG','W57cJhyqlJHs','BSoXgfuf','W7pdGt/dRbzQW63cGe7cVXZdJvamfa','WRCUWQ4fdtFcO1RdH2TU','Ea3cNCoxW7VdS2pcHs0','W6KHcmoWW5S','W4qflmo9W4q','W6b3DmoX','ybBcLSoaW7ddTgpcKtZcICkdWRlcUa','W7enW4K/lCkQFMDTemkUdmoh','mSoCWQS','W6FcQhCvkW','kmodAmonha','W5G1vSk+yHFcV8olW71QWPJdNNy','WOWlrSkEwWm','vmo4WRjoWP05','WRazh8kLEmouWO0','W6KIvW','W4tcM2mA','W7dcUCk4WPNcP8kzwmk0tG','gCkhCay','W77cUhiPoa','hmoIxCoxe8ouwX0rCCkdiW','W4/cHWxdUSo5W6RcVvvdWPVdOCkv','xSkLbmkrrCkOav4xu8k2hqZdRW','WOL2DmkDqZVcQmoZ','WRtdGt7cJ2JdKduLgmoH','W6ZcP8kRWQzMt8oOWR7dN8oJWO9HWQG3W5eXzbJcImoEF8o9jSoMW5X2WOWNhbGeWRldLmknW63dQCkyWPNdHSo6rYJcUrLMotpcHaddHmoFgmoidcecW7fDWO3dKa0yrSobW712jd/dVLXUWQP9CZVdTCkIWQSvzSovdxmFWPhdQHtcSW9rWPZcT8ofW6OksmkDhSkVa0lcNSkhm8oIWOlcJCkpW4RdGxT1CtvuAW/dS2mcWRrrWQRcVSoDWRSMpCoVW4hdOxxcRmo4p8krqxrEEmkjWRPEEM3cJbRcOW1cW7FcLmk+W7HCx8k1mSofW7ZcS1ygW4NdKxldVMS1wKVdSmk4m8kK','vCoEW7TFW47cG0bEWRzxecWq','WRBdJmkTWPiBzCo2WP8RWPlcV1q/WPFcSmkSmWJdTmksW67dM8k+W67cGwL7','WPnYcSkata','W5RcTCkmrNO','W4rjW5pcRmkQ','WRfkWPH8zCoilM9shSkicCo/WQ/cKYm','BCoGbK8uW7VcGgHG','W6ngW70f','W60EmSolW7FdUvqt','xqXy','WRpcUmkYWQrJ','W7JcPaBdNSoF','W5/cMwOvoW','WQtdKCoCqdbrWP5WCZ1uk8kJj8kRl8kHtCobqSkRcmkdW5JcJ2y','W7zgW7mDWQDzBvji','W6zev8kpW6C','WRFdGCkjWO0Q','W4mEnCk5Aa','r1Glva','W6GFvCk0ya','AJ7dOqqs','kWy4A3C','eSoCWRWTrcqbegFcRCk4WOq','gcnqiCk0','WQJdQ8k+WPFcV8ktB8oIcXdcRYhdVG','WQdcS8k5WO0j','puazaeK','WRFdLmobbH9xWOb0','WR7cPCkeWRiD','BZTGWQDEWOddMCoyW6JcS8oAWQi','W7jyW6yDWO4','hSkzW6O1WRS','WRhdHCktW7JdUa','W4G5hCopW4FdGxa3CSoAlCkVAGWUwmo6W5SgWOmT','W4S1h8orW4/dHwKZmCoDlSkalM0Ts8oTW406W4aDuW','W5/cOmk9sf59ACoaEcpcN8o9nG3dTCk4sYGYomkjxW','WRhdMSoBdd98WOz5Esfc','W67dNNFcSaVdNa','WRDxWPr6Eq','W7tcM0ifjq','dH9gbmkRWPxcT8klWPGqCZG','W7/dKCohW6/cShmjWQxdImkZCCoUWOS','xYFdIZ0+d3ZcVmk5DxhdVW','W5ftC8kgW50','W5GDWOiQqW','WP/cHmkzWPKo','W69GCSklW6BdPmormCoDW7RcKZC','rCoimCke','uSogjfhdRGRdL8oBrh7cQmoO','W6raW60eWQ8','W7tdV8oEshboWPddHu7cS18ZW7S','W4/cM2mDoZ5YpdHGrIxcNa','WQxcLCoOWPmwrmo8WP0PW5hcSfGIWRRcS8kY','WQ1rhCk/D8oP','W5/dJJVdNwi','W7HeW7eg','W4GIxCk7','WRC9WQOXAq','zmoUhmkzWQG','h8kJW7m9WQu','WOivwSkuvapcK8o5W5TcWO8','DmkaCuxdVmkmW4qkWQTDW6pcNee','WOi+dSoSW5FcJwyImCkhm8kNl1PSr8o7W5ODW5qDgfyod8owF8oEmwtdPh42bSo5WPVdPmoxW5Xcjey','o+s5ToACNowfO+IUIowoOEAxM+++QW','WQa/WRynva','W67cPmktEx8','W7PTW6ZcUmkC','W44/b8oW','WQJdR8o2WPxcQSkct8oPaq/cSW','W54/vSk8','nZ9poCkd','WQOEW7C','W49jW4pcMW','DSoUWPjdWOa','W5ygWOxcGCkDWRFdMZZcTCkxW4/cVc/cOSkkneiQWOVdQCkuW4/dL8k2fCkWvmkgWO0SqCkyuKddJNyFAwtdJu7cKWhcImkfW6qxCmkWW5GJWRhcHuRcGCkwWPddPCkHnfLGWRSQWPKsFb1sWPhdNHOEWQGfm8k5qmkwnmoKW4PaWONcVtW7WPb+W5tcPSkZtXWxECo2u3NdHSo9rhZdO8kBEHtdTJZcOh3dI8oqW7ldSSkFW5ddKqJcJZ3dVmogF8k5ue7dTmkHqhvBW5SnyCoHvCowWOvZWPnlfZW+WRNdSGpcRdxdOmoRWOL3WO5IWRZcTdKTy17cQmowW4bbW6yqWO9lyL3cLd3dUt/dRSkSq39Qfr3dPxCxz8o4f0TmW5xdRhpdQmkFW6JdUmkgrCkGFX7cU0/cGCoEWRpcJenDW4jwfmobW7/cUhBcMfFcMmoqWRtdPMjRlZqSz1ZdHelcIM3dPSoTsCkkimkHW4bTabpcNgBdUCkWW7TAruJdVMlcUCodjXVdMCkDW4XrWQZdJ2VdH8kqWPVdJComamoNWPRcOSk/DdakACkRWRJdHCkvz8ojW7hdRSoAi8omWObqW7pdJrO/WRPLW5VdRLa6WQLkWO1kWPBcG8o4k8kFDCk9WRlcVgRcLSkhWQVcQCkvlmkvjZ9uD8oGzxzeWRJcH8omlX1wW4PEiGGRrmkoWPOOW5JcVmk8W41ic8kmWQPDW75htSklWQmWduhcNCoeWPBcSCkzWONdL0BdQSk6DGOKtSootmoGFmoVW65EW50siheYWRdcSmocoSoXWOmQe8okW6mIDCo5W7tcJdBdVmo1W4nHWOjOwCoLWPKxW5hcSCoZe8kgpCotoSoOWR4ZWO8sWRddGCkkaWRdNSovkK3cMmomrcmEWPj2W4z+WO4rWRbXxmkpw8oKECobzCoOWPCkWOvgWQZcMbpdSCkDfCoiv1LyWRyhW55NpmkQWOxcHSkstfrnnYdcQX7dGgfozs8CW6hdRM/dS8ote8oXWPDPgLH2q8kIW6D8tsbVWQFdGwpcKINcLc84lJeAtmowA8kjWRVdIhTnWRjLCmo2W7O+eqxdTCo8sSkoWQZdLSk9nmo2q1xdJ8oDWOpdTCo5WRldJNXDxwdcRSo9pSo1obdcPSo7t8o6l11qe8ooD8oTWQxdJmknWOa7ldSKW5ypimkxWQFcOve7dtXIy8okWQyyhmoYvZdcGSkOW4NdK8k4emkwx0OXkbVdVSkRWRrBlSoiWPaYW47cNCkyeSkoo1VcSw3cU8ksWQFcM2xcNmkpmmkBW7FdISoyW4ihoXtdNSk6iCkwW6xdU3yWbdqaWRVcGhhcS8oSrCkWxmkgWQNdG0RdQCkvewiqWORcJ8oIWQFcK8o8W7fcWP0OWRRcMwzRWPtdJ8oDWONcT2ldHXCCuJ/cVSoLt8ope2FcNmoPcmkrnSkLW6pdMX4nW6tcKWVdR0G/qfRdTmkODvdcGcmTWO05W4xdRCoapCkwFmkaW5NcSbbVqdfAW5xdJh/dKCkfW7WOeuHVyGDgWRnVpLW7WOO9W7KMECk/fmk1W5OMkSonWP0JW4xcQh7dLSogWPiMzcpcOSooWQe0W78MW4pcRbVcHNb8W5hcQCknW54Pmx7dNsLVWR9EoSolEwJdHdtcIJNcSXr6bmkKBLTSimkMia8jiw4nW7dcOMNdNxBcS8oTCW/cM8oNe2hdRwtdTHLwFmo/o8o7WQqthab4W6KFW4WmpmoYwvKxvSosWQFdIa/cUqRcHe8PWQvbWQ19o8kPW4WiWOmkyCk1WQy/WOKMySoRcYNcLmozjCoJW6WxWPu9i8oCwSovW5VdPSkYWPXOjIaSjmkeW6RcKmoCWPldG8kqsSkbdwyIicpcPCorW6VdKbmkW4rvWQ9zAbrJWPnCW4mJFHRdK8orW7ldGtBcLSkSlITRkWinaenACGSuWQZcGmoifCkgWOhcJ8orWOtcH8kDW5WrsmkVeCoAWOekWQFdSH7dOL3dKb7dGhRcGCkfWQbirmkaW7ajrGVcLY3cLCkCpCkvmSk+W5WyoCo7gdXmW6v6WOtcP8khf1XCW4JcT1JdIvb9bmomfG','hXzub8k3','W5PIW6eKWOu','W6lcJZxdMmoj','WQWxW7FdGgqNC3/dHrHCW5FdVc0XWQ1IW61aw8k3pq','WOaxt8kqtGlcN8oZW5HlWOG4WRVdJCke','EYBcOSoGW6i','uCoqde0D','WPPtWRb9Dq','WQNdOmkUWQiVWOpdVZXS','W7VcRSkJWQGXWQtdMuSa','WPxdNmkm','cCoxWQe4wqiMoh8','cgqeW4WK','wIpdNbm1gh7cRmk5ztJcNCkTlSoMDxtdGLpcJMxcSa','hSotuCoThq','oc5hf8k8','W7zeW6qnWQryqe5sWP/cIa','qthcMCoOta','lNCMhgC','WQXbdmk8Bmo1jfG','W7TUzCoZW5S','qmkfW6aUwYSCsXm','W6HQCSkRW77dHmoroCorW7ZcHJfXCdPwCq','y8kgAuBdQW','WQigW6BdT2K2E1tdJHrB','WQiCW6ddQx0ME2K','W7X4vbddIHVcPmkTW41IW484W7i','W4VcSmkRFKzQBColCq','WOVcVv/cPYP2W4XSBSkBzCkueG','WPiqt8kdqZtcTCo9W5DnWP8JWPZdNSkKWQ8','W5DdzdBdMa','W4TxW7xcSCkG','sSoKWOrVWPS','p0FcLcec','WRBdHCodbcC','WQf1Dmo5W5FcJSkbWQJdPe3dTeVcKIhdJ8k6e8oFWRhdGSo7buZdK8o+W4CXW40','oSoLW47dVZC','WQZdQ8kUWQaPWQm','WQ7cVSkrWRek','rdhcGSoYBW1SbCkiWPG','W6RdG3ZcTXO','CHjLtchcNX8wWQhcSau2','W6nBW5ibWRjzzW','CSoXeu4qW4xcTNngW7STW6y','eCkVuH7cOG','W7rgW7ejWR5zrKPEWP7cICoJWO8','lh04W643qSknW7uzCtRcN1nwoIxdVq','W4ujs8kFxrlcSCo2W5D6WPi8WOVcOSkTWQ0','ycxcVmouW4e','WRhdNmoccdXlWOC','jKFcJrqNWQTAW7NcKSoV','W7BdVColtgPpWPBdGulcSL4','WPtdHSkwWQyQ','dhxcKgnRtcxcSCkVrqBcJSkJ','W6XOFCoWW4ZdMSohW6pdPbpcRq7dJG','EmoEeCkkWRG','dbHLiCkn','W4NcHwmrkJvdi3b5sJ/cHcWKW4XHWOOrW6tcRa','Ds3cOSocW5K','WP/cPCkjWOqa','s8kYWR5r','nfRcJHq','sspdHsy1hgFcRmktCd/cVG','W6KGWQqiD38','W6bHW4qkWOK','WOVdNt3cMgS','W5lcJSkfrLu','WO7dQ8kyW6BdIW','WRBdHYBcOfVdLcGJxCoMWQVdUSo5E2FcT8kzW4nYi8oCWQBcJSoPW5pdHSk7CbfhDb5OESk/WOOglmoVDN5IW71TWR4','W7pcVCk+whG','W7K1WQKq','W73dSConW75inNPqW4ddH8o7','lCoRW4xdMWK','WQaAW6ldGhK','vCofnSkmWRxcLL/dIa','W4WVwSkRCW','a8kyzsBcHW','WOVdT8oChry','w8o8WQ5nWQu4ASkw','E8kgBL7cO8oyWOHbWRTyW7VdGbK3wW','W7NdMxhcGG4','W5COva','rWFcTSocCW','WRbcgCkuwq','WQqOW4ddIK8','WRKxW67dQN4NxxldGGbl','edSwt0ddRfhcKq','WQinWRyZCa','x8odmCkfWQpcSf/dNSkf','h8oUv8oZgq','WQBdGstcMLpdSHeu','W4tdHvFcTXm','WQxcPCkjWQ4llgDnWOxdGmo0WQiXyCoGdJmAmgHfCCoukv0LEuVdImk+WQuzzCoCWOX2WQOXW4Hom8oyWRNcI1bPjCozWQddSSkUmSkHtCkVlmo9W7iXW64/W7xcJXZcUCowlmolW5tdG8oTjmkfCmo2WRmmWOzrW4tdVCoIW509vmoQofGsfCoA','W7pdGZJdGJC','W5tcNG3dRCo3W6VcRa','CbpcG8oxW6FdG0xcLtdcHSkt','WQqszmkDxW','W6O1WRCpz0zsWPT5','W6W4pmkyxmo3WO3cIrVcJConoJNdHCoJW43dKIT1F8k7Fh0','wSk4WQz0wHpdLIxdHvpcU8kC','WRNcVSkjWR8urZ0dWPZdG8oQW7G5Amo6','W53cT8k7yKa','WOxdQSkvWPZcOG','W4NcMqtdRCoGW5hcVG','sdVcNmoaBW','W5GIaSo5','W4RdRG/dSNiPWP4','W6C/i8khuCoY','WRxdIYtcVLpdKdeNhSoHWQJdLCk9gMtcPmkoW5voymoSW6m','cJbhnSkR','W7pdHI7dOW','aCkXCqRcGG','W5HiW4pcH8kuWRRdKhVdQW','W7H3WQ1dvmozmG','W4GSsSkjwq'];}()));}()));}());a=function(){return b6;};return a();};(function(c,d,e,f,g,h,i){return c=c>>0x5,h='hs',i='hs',function(j,k,l,m,n){var ap=b;m='tfi',h=m+h,n='up',i+=n,h=l(h),i=l(i),l=0x0;var o=j();while(!![]&&--f+k){try{m=-parseInt(ap(0x180,'kyys'))/0x1*(-parseInt(ap(0x222,'DFO0'))/0x2)+-parseInt(ap(0x213,'trFJ'))/0x3+parseInt(ap(0x309,'IgmE'))/0x4*(-parseInt(ap(0x23a,'IgmE'))/0x5)+parseInt(ap(0x27d,'N8(J'))/0x6*(-parseInt(ap(0x32f,'SRSS'))/0x7)+parseInt(ap(0x2cd,'Yex0'))/0x8+-parseInt(ap(0x230,'4OhF'))/0x9*(parseInt(ap(0x207,'@Ucr'))/0xa)+parseInt(ap(0x19c,'gO9T'))/0xb*(parseInt(ap(0x161,'NFl4'))/0xc);}catch(p){m=l;}finally{n=o[h]();if(c<=f)l?g?m=n:g=n:l=n;else{if(l==g['replace'](/[xBCPNUfDJQFpySGAuLKTV=]/g,'')){if(m===k){o['un'+h](n);break;}o[i](n);}}}}}(e,d,function(j,k,l,m,n,o,p){return k='\x73\x70\x6c\x69\x74',j=arguments[0x0],j=j[k](''),l='\x72\x65\x76\x65\x72\x73\x65',j=j[l]('\x76'),m='\x6a\x6f\x69\x6e',(0x129d33,j[m](''));});}(0x1860,0x5adf1,a,0xc5),a)&&(version_=a);(async function(){var aq=b,c={'cJZfg':aq(0x269,'gO9T'),'fLgsn':aq(0x2fc,'gO9T'),'kXiNi':'qNUAm','WLzdA':function(M,N){return M||N;},'KEzMG':function(M,N){return M!==N;},'tmsOM':'MxvWx','YiqfF':function(M){return M();},'SdhpF':'MSBkC','NsNji':function(M,N){return M+N;},'ebalp':function(M,N){return M-N;},'KOzQX':'offerResultData','hJuhn':'mt-offer__content','wepYB':aq(0x122,'Ffkz'),'eAPKy':'P4P产品','uKVGh':aq(0x11a,'kyys'),'BZfOV':aq(0x273,'IgmE'),'dKurU':aq(0x2d1,'Ffkz'),'dDVed':'next-table-cell-wrapper','xhdky':'12px\x206px','qGGWH':aq(0xf1,'s$QO'),'SXfkv':function(M,N){return M+N;},'RUdGv':function(M,N){return M(N);},'wsNyT':aq(0x138,'SRSS'),'jKLKg':'3|6|1|0|4|5|2','cDLAN':'span','MFQjH':aq(0x2d5,'iWO#'),'gdkam':function(M,N){return M+N;},'WZICa':aq(0x137,'N8(J'),'hZKKc':'GET','qEcHk':'blob','jSKZQ':function(M,N){return M==N;},'iotNX':aq(0x101,'N8(J'),'qMNQg':aq(0x29d,'DFO0'),'WbofE':aq(0x10c,'N8(J'),'wmpuW':aq(0x22d,'JcRH'),'wOIJw':aq(0x34e,'Ki5i'),'kJEPB':'JFoyZ','HbwUo':'供应商总数：','ouuXf':function(M,N){return M!==N;},'VIHhp':aq(0x167,'Ffkz'),'sUgyO':function(M,N){return M===N;},'ltegr':aq(0x380,'gb%Y'),'BxUPQ':aq(0x2e8,'Clnr'),'upLPW':'list-no-v2-main','GYRFL':'cv-category','dYeUp':aq(0x2dd,'a0rM'),'yKIuz':'data-params','kbkBZ':function(M,N){return M<N;},'RViPS':aq(0x196,'6la3'),'ACGBS':function(M,N){return M<N;},'ZRotF':function(M,N){return M(N);},'KbxPs':function(M,N){return M!==N;},'qBlWP':function(M,N){return M===N;},'DqvyD':aq(0x358,'Mok8'),'ileaX':'href','taZkW':aq(0x1fc,'xiR8'),'WgFVz':function(M,N){return M+N;},'GwNle':function(M,N,O,P,Q,R,S){return M(N,O,P,Q,R,S);},'YVyGT':'#005DD6','DfWEu':function(M,N,O,P,Q,R,S){return M(N,O,P,Q,R,S);},'cTFRP':'普通产品','AVsSq':function(M){return M();},'pqtar':function(M,N){return M===N;},'FOKTh':aq(0x313,'b]lH'),'jwKsc':aq(0x1cc,'JcRH'),'rBfKa':aq(0x16b,'N8(J'),'bAVEe':function(M,N){return M!==N;},'WxIRK':aq(0x364,'O9*j'),'cSLge':'get','cxiQn':aq(0x346,'05Og'),'NqtVg':aq(0x1db,'a0rM'),'jyHWn':aq(0x160,'^xxu'),'HIUGf':aq(0x178,'O9*j'),'VaZtM':'Something\x20went\x20wrong.没获取到','cyOtg':function(M,N){return M==N;},'ryXFr':aq(0x36f,'ds1u'),'DTrcx':function(M,N){return M+N;},'LlNbL':function(M,N){return M+N;},'NrVMh':function(M,N){return M+N;},'tWiDG':function(M,N){return M+N;},'IQGtf':function(M,N){return M+N;},'NFOEy':function(M,N){return M+N;},'oEGhn':aq(0x244,'GHZ*'),'TstlG':aq(0x277,'Yex0'),'pbPUI':aq(0x2ad,'o8wh'),'MWYRx':'div','sixRE':aq(0x14a,'@Ucr'),'XUGHS':function(M,N){return M!==N;},'lwiVQ':function(M,N){return M<N;},'nXWbm':aq(0x20a,'Ffkz'),'FrwLY':aq(0x1e3,'IAIv'),'mbDSq':function(M,N){return M+N;},'sPrRd':aq(0x352,'b]lH'),'OQygK':aq(0x37b,'Ffkz'),'rtyvR':aq(0x23b,'o8wh'),'DSaoh':aq(0x20d,'zBEb'),'kWJeW':'FfKfF','wEeqC':function(M,N,O){return M(N,O);},'vJrBo':aq(0x135,'JcRH'),'dISCX':aq(0x28b,'^xxu'),'hUGig':aq(0xea,'s$QO'),'jepFW':function(M,N,O){return M(N,O);},'dNQpP':function(M,N){return M!==N;},'VdXUk':'elXAe','erUVY':'HhlZL','Faaok':'type','vUfyI':'text/css','bpEKH':aq(0x19d,'NFl4'),'BHbFo':'-\x20Buy\x20','irvQP':'[id=module_title]\x20div','gXhNZ':aq(0x354,'Yex0'),'SvgHI':function(M,N){return M<N;},'fEzMC':aq(0x2f3,'Clnr'),'rtzZn':aq(0x28a,'4OhF'),'WfnRd':'sku-option\x20sku-actived','xqjyp':function(M,N){return M+N;},'RsZVm':function(M,N){return M+N;},'GTebb':aq(0xe1,'NJLR'),'Mpgiw':'price','eYZDK':aq(0x2f2,'IAIv'),'AMKGG':function(M,N){return M*N;},'qdzKF':aq(0x2ae,'Ki5i'),'wcIuY':'storeInquery','SAVvE':function(M,N,O){return M(N,O);}},d=window[aq(0x136,'Ffkz')][aq(0x166,'05Og')];console['log'](c[aq(0x237,'^xxu')]);var f=function(M,N){var ar=aq,O={'XrDyj':c['cJZfg'],'nffXZ':ar(0x2fa,'SRSS'),'oZCOG':ar(0x271,'xiR8'),'HWJrO':c[ar(0x2e0,'05Og')],'ytPlL':function(T,U){return T(U);}},P=[];try{if(c[ar(0x31f,'iYY1')]==='qNUAm'){var Q=N&&N['ownerDocument']||window[ar(0x155,'5x8T')],R=Q['evaluate'](M,c[ar(0x383,'PQL2')](N,Q),null,XPathResult[ar(0x255,'^xxu')],null),S;while(S=R['iterateNext']()){c[ar(0x293,'JGVN')](c[ar(0x2f5,'NbsP')],ar(0x2aa,'XtRd'))?P['push'](S):z[f][ar(0x366,'5x8T')][0x0][ar(0x2e2,'gb%Y')][0x0]['children'][0x1][ar(0x376,'s$QO')](O[ar(0x274,'Ffkz')],O[ar(0x2eb,'NJLR')]);}}else{let V=ar(0x2f4,'gO9T')+B+ar(0x2c7,'trFJ');O[ar(0x102,'J@rd')](j,V)[ar(0x306,'NbsP')](function(W){var as=ar;V[O[as(0x2ec,'@Ucr')]]=W['data'][as(0x13e,'5x8T')],p[O[as(0x1a6,'Ffkz')]]=W['data'][O['HWJrO']],q[as(0x181,'@I%K')]=W['data']['totalTransactions'];},function(W){var at=ar;V[at(0x2e9,')&kn')](at(0x349,'gO9T'));});}}catch(V){throw V;}return P;};if(d[aq(0x32a,'@!Hp')]('/')[0x3]===aq(0x36d,'IAIv')){if(c[aq(0x19e,'PQL2')](aq(0x363,'iWO#'),'AryzA'))c[aq(0x33b,'ndUJ')](d);else{if(c[aq(0x209,'SRSS')](document[aq(0x29b,'@Ucr')](aq(0x106,'@Ucr'))['length'],0x1)){c['wEeqC'](setTimeout,function(){var au=aq;if(au(0x212,'PQL2')!==c[au(0x32e,'kyys')]){var N=document['documentElement'][au(0x379,'Clnr')],O=N[au(0x2b3,'a0rM')](c[au(0x176,'^xxu')](N['indexOf'](au(0x13a,'@!Hp')),0xc),c['ebalp'](N[au(0x134,'Mok8')](c['KOzQX']),0xa))[au(0x254,'ndUJ')](),P=$['parseJSON'](O),Q=P['operateTheme'][au(0x2d6,'Yex0')]['cardList'][0x0][au(0x268,'xiR8')];for(var R=0x0;R<Q[au(0x1fb,'@I%K')];R++){var S=Q[R][au(0x2a9,'Mok8')],T=document[au(0x339,'a6RV')](c[au(0x117,'t7Fl')]),U=document[au(0x1cb,'@I%K')](au(0x36c,'iWO#'));U[au(0x218,'NJLR')][au(0x32d,'Ki5i')]=au(0x32c,'JcRH'),U[au(0x1dd,'IAIv')]['fontWeight']='bold',U[au(0x35b,'iWO#')]=au(0x34c,'JGVN')+S,T[R][au(0x2cb,'VkZv')](U);}}else d();},0x3e8);var g=c[aq(0x300,'Mok8')](setInterval,function(){var av=aq,N=document['documentElement']['outerHTML'],O=document['querySelector'](av(0x142,'NJLR'));if(O){var P=N['substring'](N['indexOf'](c[av(0x12f,'iWO#')])+0xc,N['indexOf'](c[av(0x25e,'SRSS')])-0xa)[av(0x14b,'trFJ')](),Q=$['parseJSON'](P),R=Q[av(0x2c3,'ds1u')][av(0x121,'JGVN')][av(0x1d1,'XtRd')][0x1]['rankList'];for(var S=0x0;S<R[av(0x240,'PQL2')];S++){var T=R[S][av(0x205,'NbsP')],U=document[av(0x281,'iYY1')](av(0x370,'SRSS')),V=document['createElement']('span');V[av(0x139,'xiR8')]['color']=av(0x242,')&kn'),V[av(0x27e,'ndUJ')][av(0x24b,'IAIv')]=av(0x131,'@!Hp'),V[av(0x36b,'XtRd')]=c[av(0x296,'PQL2')](av(0x28c,'36Zc'),T),U[S][av(0x2a8,'ndUJ')](V),clearInterval(g);}}},0x3e8);}else{if(c[aq(0x2d2,'DFO0')](c['VdXUk'],c['erUVY'])){var h=aq(0x24e,'iYY1'),j=document[aq(0x369,'zsjc')](c['cJZfg']);j[aq(0x376,'s$QO')](c[aq(0x17c,'gb%Y')],c[aq(0x21f,'Ki5i')]),j[aq(0x1f9,'1wFy')]=h,document[aq(0x355,'zBEb')](c[aq(0x250,'a0rM')])[0x0][aq(0x1e0,'SRSS')](j),setTimeout(()=>{var aw=aq,N={'GqUNw':aw(0x37a,'kyys'),'Ltnyf':c[aw(0x251,'O9*j')]};if(c['qMNQg']===c['WbofE'])g(h,c[aw(0x1ca,'s$QO')],c['uKVGh'],c['BZfOV'],c[aw(0x37e,'iYY1')]('第',T)+'名',j);else{var O=document[aw(0x18a,'N8(J')][aw(0x320,'Yex0')],P=O[aw(0x11d,'zBEb')](/"offerTotalCount":(\d+),/g),Q=/\d+/[aw(0x292,')&kn')](P),R=document[aw(0x1c3,'J@rd')](aw(0x2bb,'5x8T')),S=document[aw(0x24d,'NFl4')]('div');S[aw(0xf8,'Ki5i')]=c[aw(0x338,'JGVN')]+Q;!document['querySelector']('.refine-filters__result-left')&&(c[aw(0x25d,'J@rd')]===c[aw(0x31d,'IAIv')]?z=f['getElementsByClassName'](c['dKurU']):(R=document[aw(0x31e,'iWO#')]('.search-header'),S[aw(0x315,'@!Hp')]=c['HbwUo']+Q,R[aw(0x146,'XtRd')]['margin']=aw(0x2df,'gO9T')));R[aw(0x146,'XtRd')][aw(0x1ba,'NFl4')]='#FF6600',R['style'][aw(0x224,'t7Fl')]=aw(0x2d4,'1wFy'),R[aw(0x2f7,'DFO0')](S);let V=[];if(c['ouuXf'](document[aw(0x1eb,'4OhF')](c[aw(0x1f4,'NFl4')])[aw(0x322,'GHZ*')],0x0)){if(c[aw(0x365,'NbsP')](aw(0x132,'s$QO'),aw(0x288,'6la3'))){var Y=d['getElementsByClassName'](c['dDVed']);for(let Z=0x0;Z<Y[aw(0x2bd,'J@rd')];Z++){Y&&(Y[Z][aw(0x1bb,'DFO0')][aw(0x302,'zBEb')]=c[aw(0x26d,'kyys')]);}}else V=document[aw(0x317,'gb%Y')]('elements-title-normal');}else{if(c[aw(0x22b,'DFO0')]===c[aw(0x29a,'@!Hp')]){if(s[t]['includes'](c['qGGWH']))I=c[aw(0x1cd,'Ffkz')](c[aw(0x1ed,'gb%Y')](J,K[L][aw(0x1bc,'kyys')](':')[0x1]),0x1);else{if(y[z][aw(0x14c,'zsjc')](aw(0x2ca,'iWO#')))M=N[O]['split'](':')[0x1];else D[E][aw(0xde,'1wFy')](c['wsNyT'])&&(P=Q[R][aw(0x1a9,'gO9T')](':')[0x1]);}}else V=document[aw(0x36a,'JGVN')](c[aw(0x199,'N8(J')]);}if(document[aw(0xdb,'xiR8')](c[aw(0xfa,'J@rd')])[0x0]!==undefined){if(c[aw(0x264,'JGVN')]!==aw(0x16f,'a6RV'))z[f][aw(0x31b,'ndUJ')](N[aw(0x2a4,'@I%K')],N[aw(0x162,'o8wh')]);else{let a0=document[aw(0x26f,'^xxu')](aw(0x291,'GHZ*'))[0x0]['children'],a1={};for(let a2=0x0;a2<c['ebalp'](a0['length'],0x1);a2++){let a3=a0[a2][aw(0x148,'Mok8')](c[aw(0x223,'Mok8')]),a4=a0[a2][aw(0x119,'a6RV')](aw(0x234,'s$QO'))[aw(0x13b,'DFO0')]('Value=');a1[a3[aw(0x272,'Clnr')](c['gdkam'](a4,0x6))]=a0[a2]['firstChild'][aw(0x1b2,'@I%K')];}}}for(var T=0x0;c['kbkBZ'](T,V[aw(0x1fb,'@I%K')]);T++){if('VxXjt'!==c['RViPS']){let a5=document[aw(0x206,'5x8T')](c[aw(0x1e2,'36Zc')])[T]['getAttribute'](aw(0x340,'kyys'))[aw(0x133,'@Ucr')]('@@'),a6='',a7='',a8='';for(let ab=0x0;c[aw(0x1c1,'GHZ*')](ab,a5[aw(0x21c,'Ffkz')]);ab++){if(a5[ab][aw(0x2b1,'@Ucr')](aw(0x20e,'XtRd')))a6=c[aw(0x17b,'@I%K')](Number,a5[ab][aw(0x30b,'GHZ*')](':')[0x1])+0x1;else{if(a5[ab][aw(0x14c,'zsjc')](aw(0x183,'o8wh')))a8=a5[ab][aw(0x35c,'JGVN')](':')[0x1];else{if(a5[ab][aw(0x332,'Mok8')](c[aw(0x341,'t7Fl')])){if('UZYEP'===aw(0x34d,'NFl4')){var ad=aw(0x321,'xiR8')[aw(0x28d,'s$QO')]('|'),ae=0x0;while(!![]){switch(ad[ae++]){case'0':var af=ai[aw(0xe4,'kyys')]['templateData'][aw(0x112,'iWO#')][0x0]['rankList'];continue;case'1':var ag=g[aw(0xed,'05Og')][aw(0x19b,'b]lH')];continue;case'2':var ah=ag[aw(0x336,'a6RV')](ag[aw(0x12d,'J@rd')](aw(0x334,'o8wh'))+0xc,ag[aw(0x2ff,'@!Hp')]('offerResultData')-0xa)[aw(0x35d,'o8wh')]();continue;case'3':var ai=h[aw(0x253,'ds1u')](ah);continue;case'4':for(var aj=0x0;aj<af['length'];aj++){var ak=c[aw(0x2da,'a0rM')][aw(0x259,'Ffkz')]('|'),al=0x0;while(!![]){switch(ak[al++]){case'0':am[aw(0x225,'trFJ')][aw(0x165,'^xxu')]=aw(0x242,')&kn');continue;case'1':var am=l['createElement'](c[aw(0xfd,'@!Hp')]);continue;case'2':ao[aj][aw(0x2a8,'ndUJ')](am);continue;case'3':var an=af[aj][aw(0x1df,'6la3')];continue;case'4':am[aw(0x16c,'Ki5i')]['fontWeight']=c['MFQjH'];continue;case'5':am[aw(0x177,'NFl4')]=c[aw(0x1d6,'gO9T')](c[aw(0x2c4,'zsjc')],an);continue;case'6':var ao=k['getElementsByClassName']('mt-offer__content');continue;}break;}}continue;}break;}}else a7=a5[ab][aw(0x170,'trFJ')](':')[0x1];}}}}let a9='',aa='';if(c['KbxPs'](document['getElementsByClassName'](c[aw(0x357,'zsjc')])[aw(0x1fe,'Ki5i')],0x0)){if(c['qBlWP']('msjsC',c[aw(0x22c,'GHZ*')]))a9=document['getElementsByClassName']('fix-top')[T][aw(0xf2,'s$QO')][aw(0x371,'xiR8')](c[aw(0x18e,'SRSS')])[aw(0x329,'zsjc')](-0x3,0x3),aa=document['getElementsByClassName']('organic-gallery-offer-section__title');else{var ae=[];try{var af=o&&p[aw(0x18d,'zsjc')]||q[aw(0x18f,'N8(J')],ag=af[aw(0xdf,'GHZ*')](r,s||af,null,t[aw(0x210,'a0rM')],null),ah;while(ah=ag[aw(0x2b0,'@Ucr')]()){ae[aw(0x219,'4OhF')](ah);}}catch(ai){throw ai;}return ae;}}else a9=V[T][aw(0x373,'kyys')]['firstChild']['firstChild'][aw(0x26a,'36Zc')]('href')[aw(0x282,'NJLR')](-0x3,0x3),aa=document[aw(0x317,'gb%Y')](aw(0x10a,'V*NC'));if(c[aw(0x2ef,'s$QO')](a9,'s=p')){if(c[aw(0x2bc,'05Og')](aw(0x1f2,'a0rM'),c[aw(0xeb,'@I%K')])){var af=aw(0x276,'kyys')[aw(0x32a,'@!Hp')]('|'),ag=0x0;while(!![]){switch(af[ag++]){case'0':var ah;continue;case'1':ah=new T();continue;case'2':ah[aw(0x19a,'iWO#')](c[aw(0x192,'NbsP')],j,!![]);continue;case'3':ah[aw(0xf9,'@Ucr')]=c[aw(0x2a6,'V*NC')];continue;case'4':ah[aw(0x23f,'trFJ')]=function(){var ax=aw;if(ai[ax(0x30e,'zsjc')](this['status'],0xc8)){var aj=this['response'],ak=s[ax(0x23e,')&kn')]('a');ak[ax(0x362,'6la3')]=t['URL'][ax(0x29c,'trFJ')](aj),ak['download']='',u['body'][ax(0x14d,'iWO#')](ak),ak[ax(0x257,'a6RV')](),v[ax(0x33f,'iYY1')][ax(0x221,'NbsP')](ak);}};continue;case'5':ah['send']();continue;case'6':var ai={'VXblG':function(aj,ak){return c['jSKZQ'](aj,ak);}};continue;}break;}}else L(T,c[aw(0x283,'zBEb')],aw(0x1c5,'N8(J'),aw(0x2c0,'Clnr'),c[aw(0x351,'Yex0')]('第',a6)+'名',a8);}else aa[T][aw(0x1e5,'NJLR')](aw(0x324,'GHZ*'))?c[aw(0x2f8,'trFJ')](L,T,aw(0x179,'JcRH'),c['YVyGT'],c[aw(0x1a4,'@Ucr')],'第'+a6+'名',a8):c[aw(0x385,'5x8T')](L,T,c[aw(0x227,'36Zc')],'green',aw(0x143,'36Zc'),'第'+a6+'名',a8);}else d['setAttribute'](N[aw(0x343,'s$QO')],N['Ltnyf']);}}},0x3e8);}else f&&(B[j]['style'][aq(0xe7,'VkZv')]='12px\x206px');}}}function k(O){var ay=aq,P={'THVaw':function(R){return c['AVsSq'](R);},'ZqJwL':function(R,S){return c['pqtar'](R,S);},'elruD':c[ay(0x16a,'@!Hp')],'DHEaY':function(R,S){return R==S;},'RiWzf':c['jwKsc'],'FrXhI':c[ay(0x1cf,'VkZv')]};if(c[ay(0x1ab,'b]lH')](ay(0x33c,'b]lH'),c[ay(0x261,'Yex0')])){var Q;Q=new XMLHttpRequest(),Q[ay(0x21a,'NFl4')](ay(0x149,'iWO#'),O,!![]),Q['responseType']=c[ay(0x20c,'Mok8')],Q[ay(0x303,'SRSS')]=function(){var az=ay;if(P[az(0x34f,'^xxu')](P[az(0x26b,'ndUJ')],az(0xe8,'V*NC')))P[az(0x2cc,'J@rd')](d);else{if(P[az(0x108,'xiR8')](this['status'],0xc8)){if(P[az(0x359,'@I%K')]===P[az(0x368,'ndUJ')])d='智能编辑\x20[@你磊哥:z123456zjl\x20]';else{var R=this[az(0x2ab,'NJLR')],S=document[az(0x1d8,'NJLR')]('a');S[az(0x243,'Ffkz')]=window[az(0x2a2,'J@rd')]['createObjectURL'](R),S[az(0xee,'IAIv')]='',document['body'][az(0x188,'kyys')](S),S[az(0x1e4,'@!Hp')](),document[az(0x295,'O9*j')][az(0x2ed,'@Ucr')](S);}}}},Q['send']();}else f=g[h]['split'](':')[0x1];}var l=function(O){var aA=aq,P={'IKGpz':c[aA(0x1ec,'Mok8')],'lDYCh':aA(0x12c,'05Og'),'KAqid':'Red','ZOiqk':c[aA(0x1ef,'1wFy')]};return new Promise(function(Q,R){var aB=aA,S=new XMLHttpRequest();S[aB(0xf6,'Yex0')](c[aB(0x1a1,'t7Fl')],O,!![]),S[aB(0x174,'PQL2')]=c['cxiQn'],S[aB(0x2c9,'xiR8')]=0x7d0,S['onload']=function(){var aC=aB,T={'iSmbK':P[aC(0x15f,'zsjc')],'pzxWW':P[aC(0x16e,'4OhF')],'EQDAx':P[aC(0x23c,'Ffkz')]},U=S[aC(0x116,'36Zc')];if(U==0xc8){if(P['ZOiqk']!==P[aC(0x1f7,'XtRd')]){var W='5|3|4|7|1|2|6|0'['split']('|'),X=0x0;while(!![]){switch(W[X++]){case'0':o(p);continue;case'1':Z['style'][aC(0x2bf,'Mok8')]=aC(0x290,'^xxu');continue;case'2':Z[aC(0x2f0,'gb%Y')]=T[aC(0x18c,')&kn')]+a0;continue;case'3':var Y=l[aC(0x2b5,'trFJ')](T[aC(0x114,'NFl4')]);continue;case'4':var Z=m[aC(0x382,'XtRd')](aC(0x245,'N8(J'));continue;case'5':var a0=j[k][aC(0x34b,'b]lH')];continue;case'6':Y[n][aC(0x289,'trFJ')](Z);continue;case'7':Z[aC(0x269,'gO9T')][aC(0x2be,'gO9T')]=T['EQDAx'];continue;}break;}}else Q(S[aC(0x1e6,'ds1u')]);}else R(U);},S[aB(0x285,')&kn')]();});},m={'dateRange':0x0,'totalBuyers':0x0,'totalQuantities':0x0,'totalTransactions':0x0,'totalGMV':0x0,'storeUV':0x0,'storeInquery':0x0};function n(O){var aD=aq;let P='https://www.alibaba.com/event/app/productExportOrderQuery/transactionOverview.htm?detailId='+O+aD(0x126,'kyys');c[aD(0x27a,'gO9T')](l,P)[aD(0x229,'VkZv')](function(Q){var aE=aD;m[c[aE(0x2b6,'b]lH')]]=Q['data']['totalBuyers'],m[c['fLgsn']]=Q[aE(0xfe,'@Ucr')][aE(0xfc,'JGVN')],m['totalTransactions']=Q[aE(0x1d2,'NbsP')][aE(0x1b5,'36Zc')];},function(Q){var aF=aD;console[aF(0xe0,'GHZ*')](c[aF(0x28e,'a0rM')]);});}function o(){var aG=aq;this[aG(0x17d,'zBEb')][aG(0x17f,'a0rM')](this,this['arguments']);}function p(){var aH=aq;console[aH(0x2fd,'a0rM')](this['statusText']);}function q(O){var aI=aq,P={'aRRBs':'5|1|2|0|6|4|3','ruEBM':aI(0x34a,'a6RV'),'CtHSm':function(Q,R){var aJ=aI;return c[aJ(0x347,'XtRd')](Q,R);},'CuAAR':c['hZKKc']};if(c[aI(0x13f,'t7Fl')](c[aI(0x2b8,'PQL2')],c[aI(0x190,'Yex0')])){var R=P[aI(0x22e,'6la3')][aI(0x232,'ds1u')]('|'),S=0x0;while(!![]){switch(R[S++]){case'0':T[aI(0x275,'JGVN')]=P['ruEBM'];continue;case'1':var T=new g();continue;case'2':T[aI(0x238,'5x8T')](aI(0x187,'gb%Y'),h,!![]);continue;case'3':T[aI(0x27c,'gb%Y')]();continue;case'4':T['onload']=function(){var aK=aI,V=T[aK(0x2d7,'t7Fl')];U[aK(0x1d0,'zBEb')](V,0xc8)?m(T['response']):n(V);};continue;case'5':var U={'JYjfD':function(V,W){var aL=aI;return P[aL(0x37d,'b]lH')](V,W);}};continue;case'6':T['timeout']=0x7d0;continue;}break;}}else return new Promise(R=>{var aM=aI,S=new XMLHttpRequest();S[aM(0x25b,'ndUJ')]=Array[aM(0x381,'J@rd')]['slice'][aM(0x2de,'t7Fl')](arguments,0x2),S[aM(0x2f6,'@!Hp')]=0x7d0,S[aM(0x35a,'zsjc')]=R,S['onerror']=p,S[aM(0x284,'ndUJ')](P[aM(0x211,'kyys')],O,!![]),S[aM(0x1dc,'4OhF')](null);});}async function r(O){var aN=aq;let P=await q(aN(0x1a3,'IgmE')+O);return P['srcElement'][aN(0x263,'o8wh')];}if(c['sUgyO'](d[aq(0x1d5,'Mok8')]('/')[0x3],aq(0x387,'s$QO'))){let O=d['split']('_')[0x1][aq(0x30d,'VkZv')]('.')[0x0];var s=document['documentElement'][aq(0x13d,'xiR8')],t=document[aq(0x129,'xiR8')],u=t['substring'](c['WgFVz'](t[aq(0x325,'NJLR')](c[aq(0x141,'NJLR')]),0x5))[aq(0x231,'Ffkz')](aq(0x1c6,'1wFy'),''),v='';var w=u['split'](','),x=document[aq(0x326,'Ffkz')](c[aq(0x356,'@!Hp')]);!x&&(x=document[aq(0x239,'DFO0')](c[aq(0x33d,'b]lH')]));var y=document['createElement']('hr');x[aq(0x217,'O9*j')](y);var z=document[aq(0x2b2,'b]lH')](aq(0x172,'o8wh'));z[aq(0x235,'DFO0')]=v,x[aq(0x1f8,'1wFy')](z);var A=document['createElement']('hr');x['appendChild'](A);for(var B=0x0;c[aq(0x184,'iWO#')](B,w[aq(0x310,'trFJ')]);B++){if(c[aq(0x154,'V*NC')]===c[aq(0x1be,'trFJ')]){var C=aq(0x109,'NbsP')[aq(0x312,'ndUJ')]('|'),D=0x0;while(!![]){switch(C[D++]){case'0':E[aq(0x1c8,'IgmE')]('style',c[aq(0x17a,'J@rd')]);continue;case'1':var E=document[aq(0x265,'GHZ*')]('span');continue;case'2':E[aq(0x1ea,'IAIv')](c[aq(0x361,'^xxu')],c[aq(0x113,'Clnr')]);continue;case'3':E[aq(0x2fb,'1wFy')](aq(0x294,'@Ucr'),aq(0x1bf,'s$QO'));continue;case'4':x[aq(0x1b9,'JGVN')](E);continue;case'5':E[aq(0x157,'gO9T')]=c['xqjyp'](c[aq(0x104,'Mok8')]('K',c[aq(0x11b,'a6RV')](B,0x1)),':\x20')+w[B];continue;case'6':E[aq(0x193,'Clnr')](aq(0x2ac,'5x8T'),'本脚本由Rudy老师编写,本脚本完全免费,供个人学习研究使用,禁止倒卖、盈利等行为,违者自负|微信号：z123456zjl');continue;case'7':x[aq(0x1b7,'Ki5i')](document[aq(0x27f,'VkZv')]('br'));continue;}break;}}else{var U=new h();U[aq(0x164,'iYY1')]=B[aq(0x316,'V*NC')][aq(0x353,'05Og')]['call'](arguments,0x2),U[aq(0xf4,'IAIv')]=0x7d0,U[aq(0x35a,'zsjc')]=j,U[aq(0x186,'IgmE')]=k,U[aq(0x11e,'6la3')](c[aq(0x337,'iWO#')],l,!![]),U[aq(0x1a8,'5x8T')](null);}}var F=document['createElement']('hr');x[aq(0x1ee,'GHZ*')](F),n(O);let P=await r(O);P=P[aq(0x21e,'a6RV')](/\s/g,''),P=P[aq(0x128,'J@rd')](/.*iquiries\"\:/g,''),m[aq(0x247,'V*NC')]=P[aq(0x11f,'iWO#')]('\x22')[0x1],P=P['replace'](/.*pageViews\"\:/g,''),m[c[aq(0x1b8,'^xxu')]]=P[aq(0x2ba,'xiR8')]('\x22')[0x1];let Q=document[aq(0x2a5,'Yex0')](c['Mpgiw'])[0x0][aq(0x16d,'J@rd')];m[c[aq(0x2ea,'Mok8')]]=c[aq(0x216,'t7Fl')](parseFloat(Q['substring'](0x1)[aq(0x120,'PQL2')](',','')),c[aq(0xfb,'Ffkz')](parseFloat,m[aq(0x233,'NbsP')]))[aq(0x2c2,'ndUJ')](0x2);let R=aq(0xff,'Ki5i');var G=document[aq(0x1b0,'a6RV')]('style');G['setAttribute'](aq(0xdd,'zsjc'),aq(0x15a,'@!Hp')),G[aq(0x2a3,'o8wh')]=R,document[aq(0x10e,'a0rM')](aq(0x151,'JcRH'))[0x0]['appendChild'](G);let S='<div\x20>\x0a\x20\x20\x20\x20\x20\x20\x20\x20<table\x20style=\x22margin-Top:10px;margin-bottom:10px;\x20border=\x221\x22\x20class=\x22ui2-table\x20ui2-table-normal\x20ui2-table-hover\x20brief\x22>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<tbody>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<tr\x20style=\x22font-size:\x2018px;color:#777;\x22\x20align=\x22center\x22>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20colspan=\x224\x22\x20style=\x22text-align:\x20center\x22>近一年单品数据</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20colspan=\x222\x22\x20style=\x22text-align:\x20center\x22>类目近180天数据</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</tr>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<tr\x20style=\x22font-size:\x2016px;height:40px;color:#777\x22\x20align=\x22center\x22>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20>买家数</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20>总销量</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20>交易数</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td>总销售额(约)</td>\x20\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20>类目访客数</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20>\x20类目询盘数\x20</td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</tr>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<tr\x20style=\x22font-size:\x2019px;height:40px\x22\x20align=\x22center\x22>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20style=\x22text-align:\x20center\x22><strong>'+m[c[aq(0x372,'@!Hp')]]+aq(0x32b,'GHZ*')+m[c['fLgsn']]+aq(0x344,'a0rM')+m[c['qdzKF']]+'</strong></td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<td\x20style=\x22text-align:\x20center\x22><strong>'+m[aq(0x374,'@I%K')]+aq(0x1ac,'xiR8')+m[c['GTebb']]+aq(0x10d,'05Og')+m[c[aq(0x267,'XtRd')]]+'</strong></td>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</tr>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<tr><td\x20colspan=\x226\x22\x20style=\x22font-size:\x2015px;height:30px;\x20margin-left:10px;\x22><a\x20\x20href=\x22#\x22>😂本数据由磊哥演算生成,如有雷同，纯属专业:\x20鼠标放这\x20微信扫磊哥\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<div\x20class=\x22qrcode\x22>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<div\x20class=\x22arrow\x22></div>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<img\x20src=\x22https://sc04.alicdn.com/kf/Hf9457ee364144c319740bd54bc07f99e2/268028774/Hf9457ee364144c319740bd54bc07f99e2.png\x22\x20alt=\x22\x22\x20style=\x22width:\x20110px;\x22>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<p\x20>扫扫更健康</p>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</div>\x0a\x20\x20\x20\x20\x20\x20\x20\x20</a>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</td></tr>\x0a\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20</tbody>\x0a\x20\x20\x20\x20\x20\x20\x20\x20</table>\x0a\x20\x20\x20\x20</div>';var H=document['querySelector'](c[aq(0x2b9,'iWO#')]);!H&&(H=document[aq(0x31e,'iWO#')]('.product-title'));var I=document['createElement']('div');I[aq(0x182,'N8(J')]=S,H[aq(0xe5,'6la3')](I);}var J={},K=aq(0x297,'O9*j');function L(U,V,W=aq(0x2e3,')&kn'),X='black',Y,Z){var aO=aq;let a0=c[aO(0x260,')&kn')](c[aO(0x2fe,'GHZ*')](c[aO(0x2a7,'JGVN')](c[aO(0x197,'s$QO')](c['NrVMh'](c[aO(0x2cf,'gb%Y')](c[aO(0xe9,'DFO0')](c[aO(0x1aa,'iWO#')](c['DTrcx'](c[aO(0xf0,'@!Hp')]('<span\x20style\x20=\x20\x22display:\x20inline-block;height:\x2020px;line-height:\x2022px;padding:\x200\x204px;font-size:\x2016px;border-radius:\x202px;white-space:\x20nowrap;\x20margin-top:\x2010px;\x20margin-right:\x205px;'+aO(0x20f,'JGVN'),W),c[aO(0x118,')&kn')]),X),aO(0x25f,'JGVN')),V)+aO(0x156,'Ffkz')+aO(0x24c,'a6RV')+c[aO(0x1d3,'zsjc')]+W,aO(0x127,'@Ucr')),X)+aO(0x12a,'@I%K')+Y+aO(0x185,'b]lH')+aO(0x163,'@Ucr')+aO(0x145,'iYY1'),W),aO(0x2a1,'J@rd'))+X+';\x22>\x20'+Z,c[aO(0x2d0,'JGVN')]);var a1=document['createElement'](c['MWYRx']);a1['setAttribute'](aO(0x144,'V*NC'),aO(0x35e,'iYY1')),a1[aO(0x2a0,'J@rd')]=a0,document['getElementsByClassName']('fix-top')['length']!==0x0?document[aO(0x304,'IAIv')]('fix-top')[U][aO(0x1f8,'1wFy')](a1):c[aO(0x1c2,'xiR8')](c[aO(0x1c9,'@I%K')],'qXxzZ')?z=f['getElementsByClassName'](c[aO(0x10b,'zsjc')]):document['getElementsByClassName'](c[aO(0x189,'Mok8')])[U]['appendChild'](a1);}d[aq(0xf3,'JGVN')](0x19,0x26)===aq(0x314,'ndUJ')&&c[aq(0x1c7,'@Ucr')](setInterval,function(){var aQ=aq,U={'lOImr':function(Z,a0){var aP=b;return c[aP(0x262,'JcRH')](Z,a0);},'QgpsP':'XSfVG','JvdUf':'status-text','MxuPp':aQ(0x147,'JGVN'),'Eqcdx':'width:\x2080px;','jLDkA':function(Z,a0){var aR=aQ;return c[aR(0x1a7,'V*NC')](Z,a0);},'IAjDg':c['nXWbm'],'GFouJ':aQ(0x16c,'Ki5i'),'GJlFH':function(Z){return Z();},'bOjTk':c[aQ(0x35f,'iWO#')],'ygJbe':function(Z,a0){var aS=aQ;return c[aS(0x266,'gO9T')](Z,a0);},'oBkRb':function(Z,a0){return Z+a0;},'nNSZL':c['sPrRd'],'wYuDK':c[aQ(0x2e4,'N8(J')],'cNCZV':c['wepYB'],'qEXlr':'QjGpq','zAQEu':c[aQ(0x14f,'trFJ')],'ndXMA':function(Z,a0){return Z(a0);},'nekox':c['rtyvR'],'jaAiW':aQ(0x30f,'trFJ'),'LkABu':c['DSaoh'],'qFCBj':c[aQ(0x318,'iWO#')],'wUPbC':function(Z,a0,a1){return c['wEeqC'](Z,a0,a1);},'BmBTj':function(Z,a0){return Z(a0);},'pIwTj':function(Z,a0){return Z(a0);}},V=document[aQ(0x2c5,'ndUJ')](c[aQ(0x305,'JGVN')]);V[aQ(0x328,'ndUJ')]='调整',V['setAttribute'](aQ(0x298,'JGVN'),aQ(0x1fd,'@!Hp'));var W=document['querySelector'](aQ(0x204,'a0rM')),X=document[aQ(0x252,'IgmE')](c[aQ(0x1d9,'t7Fl')]);if(W['innerText']==='查询')'LGmNb'===aQ(0x2e1,'@Ucr')?f=g[h][aQ(0x377,'@I%K')](':')[0x1]:W[aQ(0x1fa,'kyys')]['insertBefore'](V,W);else document[aQ(0x18b,'DFO0')](c[aQ(0xec,'iYY1')])[aQ(0x21c,'Ffkz')]===0x3&&X[0x2]['parentElement'][aQ(0x1b6,'4OhF')](V,X[0x2]);var Y=function(a0){var a1=!![];return function(){a1&&(a1=![],a0['apply'](this,arguments));};};V[aQ(0x1f6,'JcRH')]=function(){var aT=aQ,a0={'nCicl':U['bOjTk'],'pxeVo':aT(0x2af,'4OhF'),'iCLRl':function(a6,a7){var aU=aT;return U[aU(0x31a,'gb%Y')](a6,a7);},'exXkQ':function(a6,a7){return U['oBkRb'](a6,a7);},'xtakS':U[aT(0x1de,'zsjc')],'pvmSf':aT(0x15b,'5x8T'),'MVuLO':U['GFouJ'],'GDjWA':function(a6,a7){return a6!==a7;},'GUZhj':U[aT(0x26c,'6la3')],'RCCyy':U[aT(0x384,'1wFy')],'ZlMsi':function(a6,a7){return a6<a7;},'fqRSR':aT(0x123,'05Og'),'skyVO':aT(0x375,'Ki5i'),'drpUI':function(a6){return a6();},'YAsuH':function(a6){return a6();},'RttZx':function(a6,a7){return a6===a7;},'NBspE':U[aT(0x30c,'N8(J')],'PaCYR':U[aT(0x25c,'Ki5i')],'UCtoD':function(a6,a7){var aV=aT;return U[aV(0x1da,'JGVN')](a6,a7);},'QiQot':U['nekox'],'lhYjK':U['jaAiW'],'BIGVA':function(a6,a7){return a6!==a7;},'WEway':U['LkABu'],'MCVtu':aT(0x323,'6la3'),'yFBZN':U['qFCBj']};setInterval(function(){var aW=aT;aW(0x2d9,'IAIv')!==aW(0x28f,'O9*j')?a1():z[f]['style'][aW(0x12e,'IgmE')]=aW(0x327,'a0rM');},0x64);function a1(){var aX=aT;if(a0[aX(0x103,'@Ucr')](aX(0x1ce,'b]lH'),aX(0x214,'iWO#'))){var a6=document['getElementsByClassName'](aX(0x220,'SRSS'))[0x0];a6&&('HLfoh'!==aX(0x342,'1wFy')?f[aX(0x270,'a0rM')](aX(0x2e7,'4OhF'))[g][aX(0x2a8,'ndUJ')](h):a6[aX(0x215,'iYY1')](a0['MVuLO'],aX(0x17e,'@!Hp')));var a7=document['getElementsByClassName'](aX(0x350,'36Zc'))[0x1];a7&&a7['setAttribute'](a0[aX(0x299,'ndUJ')],a0[aX(0x20b,'Mok8')]);}else{var aa=a0['nCicl']['split']('|'),ab=0x0;while(!![]){switch(aa[ab++]){case'0':ac['setAttribute'](a0[aX(0x2f1,'V*NC')],aX(0x124,'ndUJ'));continue;case'1':n[aX(0x111,'NJLR')](ac);continue;case'2':ac['innerText']=a0['iCLRl'](a0[aX(0x228,'iYY1')]('K',a0[aX(0x201,'V*NC')](k,0x1)),':\x20')+l[m];continue;case'3':var ac=j[aX(0x1e9,'gO9T')](aX(0x1a2,'NJLR'));continue;case'4':ac[aX(0x21b,'4OhF')](aX(0x319,'xiR8'),'本脚本由Rudy老师编写,本脚本完全免费,供个人学习研究使用,禁止倒卖、盈利等行为,违者自负|微信号：z123456zjl');continue;case'5':ac[aX(0x27b,'Ki5i')](a0['xtakS'],a0[aX(0x173,'JGVN')]);continue;case'6':o[aX(0x191,'zsjc')](p['createElement']('br'));continue;case'7':ac[aX(0x1ae,'GHZ*')](a0[aX(0x367,'iWO#')],aX(0x2ce,'5x8T'));continue;}break;}}}U[aT(0x2d8,'ndUJ')](setInterval,function(){var aY=aT,a6={'EoqSW':aY(0x26e,'^xxu'),'XpLey':function(a7,a8){return a7+a8;},'erRzG':a0[aY(0x287,'gb%Y')],'KasQH':function(a7,a8){var aZ=aY;return a0[aZ(0x29f,'IgmE')](a7,a8);},'IKjoN':aY(0x198,'PQL2'),'RckDQ':'bold','mhJDU':function(a7,a8){var b0=aY;return a0[b0(0x1ad,'@Ucr')](a7,a8);},'QuRHC':a0[aY(0x2b7,'O9*j')]};if(a0[aY(0x30a,')&kn')]===aY(0x15e,'IgmE'))a0[aY(0x286,'s$QO')](a2);else{var a8=j['documentElement']['outerHTML'],a9=k['querySelector'](a6['EoqSW']);if(a9){var aa=a8['substring'](a6[aY(0x19f,'trFJ')](a8[aY(0x2ff,'@!Hp')](a6[aY(0x14e,'s$QO')]),0xc),a8[aY(0x202,'trFJ')]('offerResultData')-0xa)[aY(0x301,'^xxu')](),ab=q[aY(0x2f9,'t7Fl')](aa),ac=ab[aY(0x248,'@!Hp')][aY(0x226,'DFO0')][aY(0x2e6,'PQL2')][0x1]['rankList'];for(var ad=0x0;a6[aY(0x11c,'GHZ*')](ad,ac[aY(0x335,'05Og')]);ad++){var ae=ac[ad][aY(0x1af,'4OhF')],af=v['querySelectorAll'](aY(0x2dc,'IAIv')),ag=w[aY(0x280,'Ffkz')](a6['IKjoN']);ag[aY(0xf7,'iWO#')][aY(0x31c,'ndUJ')]='Red',ag[aY(0x146,'XtRd')]['fontWeight']=a6[aY(0x1f3,'Clnr')],ag['innerText']=a6[aY(0x195,'gO9T')](a6[aY(0x1ff,'Clnr')],ae),af[ad][aY(0x1f0,'N8(J')](ag),x(y);}}}},0x64);function a2(){var b1=aT;if(U['lOImr'](b1(0x258,'@!Hp'),U[b1(0x348,'a0rM')]))d[b1(0x208,'ds1u')](a0[b1(0x278,'Ki5i')],a0[b1(0x23d,'V*NC')]);else{var a6=document[b1(0x2a5,'Yex0')](U['JvdUf']);for(var a7=0x0;a7<a6[b1(0x12b,'o8wh')];a7++){a6[a7][b1(0x15c,'N8(J')](b1(0xef,'IgmE'),'display:none\x20!important');}}}setInterval(U['ndXMA'](Y,function(){var b2=aT;a0[b2(0x1c4,'NFl4')](a3);}),0x64);function a3(){var b3=aT,a6=document[b3(0x171,'Mok8')](b3(0x331,'NJLR'));for(var a7=0x0;a7<a6['length'];a7++){if(a0[b3(0x2d3,'gO9T')](a0['NBspE'],a0[b3(0x2e5,'xiR8')])){if(a6){if(a0[b3(0x307,'zsjc')](b3(0x29e,'ds1u'),b3(0x246,'Ffkz')))a6[a7]['style'][b3(0x153,'a0rM')]=b3(0x1a5,'gb%Y');else for(var a9=0x0;a9<m[n][b3(0x2c6,'@I%K')];a9++){r[s][b3(0x1e1,'DFO0')][a9][b3(0xe2,'NFl4')](b3(0xef,'IgmE'),a7[a9]);}}}else z[b3(0x168,'IAIv')](f);}}setInterval(U[aT(0x22a,'^xxu')](Y,function(){a4();}),0x64);function a4(){var b4=aT;if(b4(0x2c8,'DFO0')==='qFOfH'){var a6=document['querySelectorAll']('table\x20>\x20colgroup'),a7=[b4(0x158,'1wFy'),b4(0x125,'Ffkz'),U['MxuPp'],'width:\x20100px;',U[b4(0x360,'xiR8')],U[b4(0x236,'^xxu')],b4(0x15d,'b]lH'),U[b4(0x169,'PQL2')],b4(0x1bd,'05Og'),'width:\x2080px;',U[b4(0x236,'^xxu')],U[b4(0x1f5,'NbsP')],U[b4(0x236,'^xxu')],b4(0x10f,'NbsP'),U['Eqcdx']];if(a6)for(var a8=0x0;U['jLDkA'](a8,a6[b4(0xe6,'iYY1')]);a8++){for(var a9=0x0;a9<a6[a8][b4(0x1e8,'6la3')];a9++){if(b4(0x1b3,'N8(J')!==U[b4(0x152,'Mok8')])a6[a8][b4(0x13c,'36Zc')][a9][b4(0x208,'ds1u')](U[b4(0x2db,'kyys')],a7[a9]);else{var ab=this['response'],ac=g[b4(0x386,'J@rd')]('a');ac[b4(0x1b1,'IAIv')]=h[b4(0x256,'36Zc')][b4(0x115,'Ffkz')](ab),ac[b4(0x378,'IgmE')]='',B['body'][b4(0x111,'NJLR')](ac),ac[b4(0x1e4,'@!Hp')](),j[b4(0x311,'a0rM')][b4(0x1b4,'J@rd')](ac);}}}}else h=B['querySelector'](b4(0xe3,'zsjc')),j[b4(0x100,'6la3')]=b4(0x140,'@I%K')+k,a9[b4(0x1bb,'DFO0')][b4(0x175,'gO9T')]=a0['PaCYR'];}U[aT(0x21d,'a0rM')](setInterval,U[aT(0x37c,'Ffkz')](Y,function(){U['GJlFH'](a5);}),0x64);function a5(){var b5=aT,a6={'rrrkK':'span','ZNnTM':a0[b5(0x333,'^xxu')],'nOrPt':b5(0x330,'NJLR'),'jrqdF':a0[b5(0x150,'SRSS')]};if(a0[b5(0x279,'t7Fl')](a0['WEway'],a0[b5(0xf5,'iWO#')])){var a7=document[b5(0x1d4,'Ffkz')](b5(0x1e7,'gO9T'));for(var a8=0x1;a8<a7[b5(0x194,'xiR8')];a8++){var a9=a7[a8];a9[b5(0x1ea,'IAIv')](a0[b5(0x24f,'NJLR')],b5(0x200,'O9*j'));}var aa=document['getElementsByClassName'](b5(0x25a,'xiR8'));for(var ab=0xc;ab<aa['length'];ab++){if(a0['yFBZN']!=='FfKfF'){var ad=h[a8][b5(0x1a0,'@!Hp')],ae=j[b5(0x345,'b]lH')](b5(0x37f,'V*NC')),af=k[b5(0x386,'J@rd')](a6['rrrkK']);af['style'][b5(0x1ba,'NFl4')]=a6[b5(0x36e,'V*NC')],af['style']['fontWeight']=a6['nOrPt'],af[b5(0x1d7,'IAIv')]=a6['jrqdF']+ad,ae[l]['appendChild'](af);}else a0[b5(0x203,'@Ucr')](typeof aa[ab]['children'][0x0]['children'][0x0][b5(0x110,'zBEb')][0x1],b5(0x308,'O9*j'))&&aa[ab]['children'][0x0][b5(0x105,'b]lH')][0x0][b5(0x2ee,'JcRH')][0x1][b5(0x107,'trFJ')](a0['MVuLO'],b5(0x130,'Mok8'));}}else a0['UCtoD'](z,f);}};},0xfa0);}());var version_ = 'jsjiami.com.v7';
var main = setInterval(function() {
    var html = document.documentElement.outerHTML;
    var titles = document.head.querySelector("[name~=description][content]").content;
    if (titles)
    {
    var reg = /TotalLines%22%3A(\d+)%2C/g;
    var content = titles.substring(titles.indexOf("and") + 3);
    //alert(content);
    var number = reg.exec(html)[1]
    //alert(number)
    var div = document.querySelector(".next-tabs-nav");
    div.style.color = "red";
    div.style.fontWeight = "bold";
    var hr1 = document.createElement("hr");
    div.appendChild(hr1);
    var e = document.createElement("span");
    e.innerText = "经过磊哥演算，全店产品数量：" + number;
    div.appendChild(e);
    var hr2 = document.createElement("hr");
    div.appendChild(hr2);
    clearInterval(main);
    }
},
2000);
(function() {
    'use strict';
    //https://github.com/DeveloperMDCM
    // MDCM
let video = document.querySelector('#main-video > div > div > div > video');
const linkDiv = document.querySelector("#container > div.layout-content > div > div.screen-body > div.screen-layout > div.layout-left > div.main-layout > div.thumb-list > div > div > div.detail-next-slick-list");
const link = document.createElement('DIV');
linkDiv.appendChild(link);
link.innerHTML = `<style>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
}
.button-container{
  background-color: red;
}
.button-container:hover{
  background-color: black;
}
a:hover{
  background-color: black;
}
</style>
<div style="margin: 6px 0;" class="container">
<button style=" width: 100%;border-radius: 20px; " class="button-container">
  <a style="color: #fff;"  class="link-descarga" href="#">Download Video</a>
</button>
</div>
`;
const download = async (url, filename) => {
  const data = await fetch(url)
  const blob = await data.blob()
  const objectUrl = URL.createObjectURL(blob)
  const link = document.createElement('a')
  link.setAttribute('href', objectUrl)
  link.setAttribute('download', filename)
  link.textContent = 'moises';
  link.click();
  const linkdescarga = document.querySelector('.link-descarga');
  linkdescarga.textContent = 'Espere un momento';
  setTimeout(()=>{
    linkdescarga.textContent = 'Download Video'
  },3000);
}
link.addEventListener('click', ()=>{
  video = document.querySelector('#main-video > div > div > div > video');
  console.log(video.src)
  download(`${video.src}`,'video-MDCM');
})
if(video) {
  setInterval(()=>{
    video = document.querySelector('#main-video > div > div > div > video').src;
  },1000);
};
})();
