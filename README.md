# 管理Sass项目文件结构

> 本文由大漠根据Hugo Giraudel的《Architecture for a Sass Project》所译，整个译文带有我们自己的理解与思想，如果译得不好或有不对之处还请同行朋友指点。如需转载此译文，需注明英文出处：http://www.sitepoint.com/architecture-sass-project。
> - ——作者：[Hugo Giraudel](http://www.sitepoint.com/author/hgiraudel)
> - ——译者：[大漠](http://www.w3cplus.com/)

回想起来，我们以前做的事情主要是围绕着CSS打转。你是否还记得，你曾彻夜不眠的在努力写CSS。Year!写了上千行的代码——通常是写得不好——为了解决一些IE的bug，或者为了找到一个属性值，我们不得不努力去寻找这样的一个值。

*****

我的小伙伴们，那些苦逼的日子就将过去了。CSS处理变得更有趣，也更复杂。现在我们有CSS预处理器、响应式设计、渐进增强、优雅降级，和其他一些时尚的东西。可以说，CSS变得比以往任何时候都更加强大。

*****

> CSS变得更有趣，更复杂。——@[Hugo Giraudel](http://www.sitepoint.com/author/hgiraudel)

所以我们有很多东西需要处理，这样一来，如何组织项目文件就变得非常的重要。我想大家都同意这样的观点，但实现起来并不太容易。所以我写了这篇文章，将会告诉你应该怎么去想，比告诉你怎么做要更好，否则，我就离开你了。

### 构建你的结构体系

CSS预处理器的特点之一是可以把你的代码分割成很多个文件，而且不会影响性能。这都要归功于Sass的@import命令，只要在你的开发环境下，你调用不管多少文件，最终将编译出一个CSS样式文件。

> 多个文件中开发，最终合并输出一个文件。——@Bruce Lee

开始将你的CSS文件分割成多个文件和文件夹。正如我的一位导师说的“任何事物都有其正确的地方，每个地方都有其正确的事”。那么，这也是我喜欢做的事。

### 文件夹构建

文件夹的创建是必不可少的。就算在家里，你也不会把所有的纸张放在一个盒子里。你可能会使用一个文件夹。一个用于房子上，一个用于银行，一个用于账单等等。

你在创建CSS的架构的时候也应该如此：你不只是把所有的Sass文件放在一个文件夹下，你会将他们分类。

下面的示例屏示的是我将如何组织我的Sass文件：

```
sass/
|
|– base/
|   |– _reset.scss       # Reset/normalize
|   |– _typography.scss  # Typography rules
|   ...                  # Etc…
|
|– components/
|   |– _buttons.scss     # Buttons
|   |– _carousel.scss    # Carousel
|   |– _cover.scss       # Cover
|   |– _dropdown.scss    # Dropdown
|   |– _navigation.scss  # Navigation
|   ...                  # Etc…
|
|– helpers/
|   |– _variables.scss   # Sass Variables
|   |– _functions.scss   # Sass Functions
|   |– _mixins.scss      # Sass Mixins
|   |– _helpers.scss     # Class & placeholders helpers
|   ...                  # Etc…
|
|– layout/
|   |– _grid.scss        # Grid system
|   |– _header.scss      # Header
|   |– _footer.scss      # Footer
|   |– _sidebar.scss     # Sidebar
|   |– _forms.scss       # Forms
|   ...                  # Etc…
|
|– pages/
|   |– _home.scss        # Home specific styles
|   |– _contact.scss     # Contact specific styles
|   ...                  # Etc…
|
|– themes/
|   |– _theme.scss       # Default theme
|   |– _admin.scss       # Admin theme
|   ...                  # Etc…
|
|– vendors/
|   |– _bootstrap.scss   # Bootstrap
|   |– _jquery-ui.scss   # jQuery UI
|   ...                  # Etc…
|
|
`– main.scss             # primary Sass file
```

正如你所看到的，在根目录底下只有一个`main.scss`文件，其他`.scss`文件都根据不同的分类放在对应的文件夹中，只是这些.scss文件前面都有一个下划线(_)，用来告诉Sass，这些`.scss`文件只是[局部](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#partials)，不通过`@import`是不应该被编译出`.css`文件。事实上，它们是导入和合并文件的[基本文件](https://gist.github.com/HugoGiraudel/8615243)而以。

> 一个文件可以解决所有问题，一个文件可以找到他们，一个文件给他们带来了所有的一切，Sass只是将他们合并在一起。——@J.R.R. Tolkien

接下来，我们依次来看结构中的每一个文件目录。

#### Base

`base/`文件夹包含了一些有关于你的项目中一些模板相关。在这里，你可以看到`reset`样式(或者`Normalize.css`,或者其他)，也有一些关于文本排版方面的，当然根据不同的项目会有一些其他的文件。

- _reset.scss或_normalize.scss
- _typography.scss

#### Helpers

`helpers/`文件夹（有的地方也称其为`utils/`）主要包含了项目中关于Sass的工具和帮助之类。在里面放置了我们需要使用的_`function.scss`，和`_mixin.scss`。在这里还包含了一个`_variables.scss`文件（有的地方也称其为`_config.scss`），这里包含项目中所有的全局变量（比如排版本上的，配色方案等等）。

- _variables.scss
- _mixin.scss
- _function.scss
- _placeholders.scss(也有称为_helpers.scss)

#### Layout

`layout/`文件夹(有时也称为`partials/`)中放置了大量的文件，每个文件主要用于布局方面的，比如说"header"，"footer"等。他也会包括`_grid.scss`文件，用来创建网格系统。

- _grid.scss
- _header.scss
- _footer.scss
- _sidebar.scss
- _forms.scss

导航文件（`_navigation.scss`）文件放在这里也有意义，虽然我将他放在了`components/`文件夹中。但是我想将其放在`layout/`文件夹中更好些，当然最后还是由你自己来决定。

#### Components

对于一些小组件，都放在了`components/`文件夹（通常也称为`modules/`），`layout/`是一个宏观的（定义全局的线框），`components/`是一个微观的。它里面放了一些特定的组件，比如说`slider`，`loading`，`widget`或者其他的小组件。通常`components/`目录下的都是一些小组件文件。

- _media.scss
- _carousel.scss
- _thumbnails.scss

#### Page

如果你需要针对一些页面写特定的样式，我想将他们放在`page/`文件夹中是非常酷的，并且以页面的名称来命名。例如，你的首页需要制作一个特定的样式，那么你就可以在`page/`文件夹中创建一个名叫`_home.scss`文件。

- _home.scss
- _contact.scss

根据你自己的布署，你可以根据自己的需求调用这些文件，避免与其他样式文件合并在一起。这真的主取决于你自己，在我工作的地方，我是不允许这样的事情发生，只在需要的页面调用需要的文件。比如说，我们首页有一个特定的布局样式，编译出来的CSS大约有200行代码。为了防止每个页面加载这些代码，我只在主页文件上引用这个文件。

#### Themes

如果你像我一样要为一个大型的网站制作多个主题，那么有一个`theme/`文件夹是非常有意义的。你可以把主题相关的文件放在这个文件夹中。这绝对跟具体的项目有关，你只要觉得跟主题相关的，有必要引入。

- _theme.scss
- _admin.scss

#### Vendors

最后一个但并非不重要，创建vendors/文件夹，主要用来包含来自外部的库和框架的CSS文件。比如Bootstrap，jQueryUI，FancyCarouselSliderjQueryPowered等等。把这些文件放在同一个文件夹中，你可以说，嘿，这些代码不是我的，不是我写的，跟我无关。

例如：

- bootstrap.scss
- jquery-ui.scss
- select2.scss

从另一个角度来说，在我平时工作中，还创建了一个`vendors-extensions/`文件夹，用来放置一些覆盖从外部引入进来的库和框架中的小组件。例如，我们可以在`_bootstrap.scss`文件中用来覆盖Bootstrap框架中的一些小组件。这为了避免和外部直接引来的组件升级造成的冲突，或许这不是一个很好的方案。

大致就是这些，但不同的项目可能会不一样，但我可以肯定，你们都有了这样的一个概念。在文件夹中嵌套一个文件夹，这样的做法我一直不太反对，但我不太喜欢这样的方式。我发现，在大多数情况之下，只需一个层级就足足够，既保证结构的简洁与清晰，而且不复杂。但话又说回来，如果你觉得你的项目有必要嵌套更深层次的文件夹，你也可以自由的发挥。

**温馨提示：**如果你觉得你的架构并不能向大家说明`SCSS`文件夹的架构，你可以在根目录下创建一个`README.md`文件（或者在`main.scss`文件中一步一步说明）解释。

### 文件很酷？

有一个问题常被人问到“多少文件才算是很多文件呢？”我常回答“再多文件都不算多”。拆分成多个文件的宗旨是帮助你组织你的代码。如果你觉得某事值得拆分成多个文件，可以自由的拆分。正如[CHRIS COYIER](http://chriscoyier.net/)在《[Sass Style Guide](http://css-tricks.com/sass-style-guide/)》中所说：

> 拆分成尽可能多的小文件是有道理的。——@[CHRIS COYIER](http://chriscoyier.net/)

不过，我建议不把单个组件拆分成多个文件，除非你有很好的理由这样做。通常我更倾向于一个组件一个文件。俗话说“没有更多，只有更少”。用一个简洁语义化的名称，用来表示模块的名称。这样我们就可以通过查找名称找到你需要的东西。

#### 总结

本文所有内容都是基于我当年在法国Crédit Agricole银行做前端（唯一一前端）的工作经验。针对于各人，有各自的情况和经验，可以有不同的方法。

如果我们能给构建一个Sass项目挑选一个黄金法则，它可能会简单一些：就如捡东西的一个道理。如果做为一个团队，项目的结构要确认每个人用得都舒服，让大家都要知道是怎么一回事。

你对构建Sass项目架构有任何想法和建议，我们都非常想听听。

> 能力越大，责任越大。——@Aquaman

**译者手语：**整个翻译依照原文线路进行，并在翻译过程略加了个人对技术的理解。如果翻译有不对之处，还烦请同行朋友指点。谢谢！

如需转载烦请注明出处：

> 英文原文：http://www.sitepoint.com/architecture-sass-project

> 中文译文：http://www.w3cplus.com/preprocessor/architecture-sass-project.html
