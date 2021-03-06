## styled-components
> yarn add styled-components
实现样式私有

## react-transition-group
> yarn add react-transition-group
*引入模块 import { CssTransition } from 'react-transition-group'*
```
<CSSTransition 
  timeout={200} 
  in={this.state.focused}
  classNames="slide">
    <NavSearch className={this.state.focused ? 'focused': ''}
    onFocus={this.handleInputFocus}
    onBlur = {this.handleInputBlur}>
    </NavSearch>
 </CSSTransition>
 ```

包裹需要使用动画效果的dom结构 再NavSearch被渲染之前 会添加slide这个类名 并再类名写样式

## 实际项目开发使用store流程
 1. 新建仓库
 2. 新建状态处理函数（reducer) 根据 action 对象的type 来更新状态.
 3. 使用store进行数据处理 yarn add react-redux
```
import { Provider } from 'react-redux'
<Provider store={store}> //连通store仓库
  <Header />
</Provider>
```
 4. 组件中(以header为例)
 ```
//使Header与store建立连接 
import {connect} from 'react-redux'
 
//取store数据 将仓库中store映射到props
const mapStateToProps = (state) => {
  return {
    focused: state.focused
  }
}

// store.dispatch ===> props
const mapDispatchToProps = (dispatch) => {
  return {
    handleInputFocus(){
      const action = {
        type : 'search_focus'
      }
      dispatch(action)
    },
    handleInputBlur() {
      const action = {
        type : 'search_blur'
      }
      dispatch(action)
    }
  }
}
export default connect(mapStateToProps, mapDispatchToProps)(Header)
 ```

## import { fromJS } from 'immutable'
>immutable对象是不可直接赋值的对象，它可以有效的避免错误赋值的问题
  fromJS将一个JS对象变为immutable对象

## 动态添加背景图
```
//组件中
<RecommendWrapper>
  <RecommendItem imgUrl="http://cdn2.jianshu.io/assets/web/banner-s-club-aa8bdf19f8cf729a759da42e4a96f366.png">
  </RecommendItem>
  <RecommendItem imgUrl="http://cdn2.jianshu.io/assets/web/banner-s-7-1a0222c91694a1f38e610be4bf9669be.png">
  </RecommendItem>
</RecommendWrapper>
// style.js
export const RecommendItem = styled.div`
  width: 280px;
  height: 50px;
  border-radius: 4px;
  margin-bottom: 6px;
  background: url(${props => props.imgUrl});
  background-size: contain;
`
```

## 回到顶部
> window.scrollTo(0,0)

## 标签不被转义为字符串（数据存储HTML标签）
> 使用该标签 <Content dangerouslySetInnerHTML={{__html:this.props.content}}></Content>

## react-loadable
> 异步组件加载 解决单页面应用首次加载速度慢（按需加载）