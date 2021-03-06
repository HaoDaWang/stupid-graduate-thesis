# 基于 Golang 的分布式酒店客房管理系统设计与实现

### 桌面软件带来的窘境

1973 年创造出了第一台带有 GUI 的操作系统 Alto，这是 GUI 诞生的标识，带有 GUI 的桌面软件发展到今天，我们不得不承认它带来的好处，一台具有图形化界面的计算机和一个带有图形化界面的软件确实能够解决很多问题，比如上个世纪 90 年代流行的电子邮件，当时的电子邮件软件相当流行，但是同时也有很多冗余的功能，很多时候，我只想要收发邮件，不想要其他的一些我用不上的功能，但是我不得不去下载它，然后学习它的一些功能，这样带来的是一些不必要的学习成本。

第二个窘境是，使用成本，我们使用它的前提是把它下载下来，这无疑增加了使用的成本。很多时候，我们想要的不是做一些额外的工作，而是想实现一些开箱即用的功能。比如 web app，当然这是后话了。

第三个窘境就是 bug 的修复，开发者无时无刻都在想如何提升用户体验，最被开发者们畅谈的是，如何解决 bug，版本发布与更新。在桌面软件环境中，你想到了一个新的好点子，或者是用户发现了一个致命的 bug，都得等到下一次版本发布的时候，推送给用户更新，在这之前，可能还没有 Notifaction，必须等待用户主动下载，如果用户不去下载，那这个致命的 bug 就会是一个隐患一直在用户的计算机上，这种体验是相当不好的，bug 不能及时修复，Feature 不能及时发布，bug 的修复周期变得冗长，其实这些都是开发者和用户都不希望看到的东西。

### 客房信息管理系统的现状

很多时候，酒店信息管理系统的功能都是集成的，前台接待 IMS 和客房 IMS 以及其他的 IMS 是集成在一起的，软件的开发商为了提供一条龙式的服务，希望酒店使用他们的前台 IMS 不得不一起连带客房 IMS 一起买下来，酒店也希望不那么折腾，毕竟酒店只是一个用户。但是这样带来的问题是，依赖于同一个 service provider，如果客房 IMS 出现了一个致命的 bug，不得不等待开发商同下一次的大版本一起发布下去，同时，酒店信息管理系统有时候并不需要这样做不是吗，我们希望的是它们的耦合被降到很低，客房 IMS 出现的 bug 被立即修复，不用再等到下一次的版本发布，我们也不想再跟其他的 IMS 捆绑在一起。我们为什么要引入 web app 这就是原因。

现在是 web 2.0 的时代，尽管许多酒店 IMS 还在继续维护，继续为用户提供技术支持，但是 UI 也是百年不会更新，这样带来的是极低的用户体验，很多强大的多的 IMS 的 UI 好像还活在上个世纪，真正明白用户的需求这才是最重要的，所以才会有那么多的软件开发模型。我们希望的是，渐进式的更新，想到一个好点子，一个漂亮的 UI 马上就能在线上产品上反映出来，不用等到下一次版本的发布，并且也希望用户和开发者的距离可以尽可能的近，用户的反馈可以立即被实现，被推送到现在的线上版本，甚至我们希望，在不停止服务的前提下，实现无缝的更新切换。现在不是上个世纪的 static page 的时代，用户才是至关重要的存在。

### Web App 的引入

