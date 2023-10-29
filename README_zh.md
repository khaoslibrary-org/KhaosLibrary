<p align="center">
 <img width="100px" src="khaos.png" align="center" alt="GitHub Readme Stats" />
 <h2 align="center">Khaos Library</h2>
 <p align="center">一个基于区块链的元数据图书馆</p>

  <p align="center">
    <a href="/README.md">English</a> |
    <a href="/README_zh.md">中文版</a>
  </p>
</p>

## Features

- 任何人或组织都无需注册即可自由地查询和使用数据
  -  使用json-ld格式的开放数据，更易于使用，以及兼容图书馆的MARC等编码格式
  -  可以通过isbn/oclc等查询书籍信息
  -  可以通过imdb/tmdb id等查询电影信息
  -  etc
- 包含人类各种CreativeWork 的元数据（如：Book/Movie/Music/Game/舞台剧）
  - 书籍的isbn、出版、封面、作者等信息
  - 电影的评级、上映、海报、导演、演员等信息
  - etc
- 永久存储
- 抗审查
- 任何人或组织可编辑和贡献数据


## 结构和模型
重用[schema.org](https://schema.org)词表，使用**FRBR**模型建模。
详见：

## 查询
目前可以通过Arweave的官方或非官方Gateway查询。
[Doc](doc/Query.md)
查询示例:
[通过isbn查询书籍元数据](doc/Query_zh.md#search-book-metadata-by-isbn)
[通过书籍名称查询书籍元数据](doc/Query_zh.md#search-book-metadata-by-book-name)
[通过作者名查询书籍元数据](doc/Query_zh.md#search-book-metadata-by-author)
[通过其他标识查询书籍元数据](doc/Query_zh.md#search-book-metadata-by-other-identifiers)
[获得书籍详细元数据](doc/Query_zh.md#get-more-details)

## 贡献
### 数据结构建议
- 请提issue
### 贡献数据
- 如果你拥有大量的书籍/电影/游戏/音乐等数据，请邮件或者matrix联系我。
- 如果你希望拥有创建和编辑条目的权限，请耐心等待第一阶段的开发完成


## License
cc-by-4.0
