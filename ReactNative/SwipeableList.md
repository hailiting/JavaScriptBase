~~~
import React, { Component } from 'react';
import {
  Platform,
  StyleSheet, // 样式绑定
  Text,
  View,
  FlatList, // list菜单
  RefreshControl, // 下拉刷新控制
  ActivityIndicator, //  loading
  SwipeableFlatList, // 右滑菜单 
  TouchableHighlight,  // 按钮组件
} from 'react-native';

type Props = {};
const CITY_NAMES = ['北京', '河南省', '安徽省', '福建省', '甘肃省', '贵州省', '海南省', '河北省', '黑龙江省', '湖北省', '湖南省', '吉林省', '江苏省', '江西省', '辽宁省', '青海省', '山东省', '山西省', '陕西省', '四川省', '云南省', '浙江省', '台湾省', '广东省',]
export default class SwipeableListViewDome extends Component<Props> {
  constructor(props) {
    super(props);
    this.state = {
      isLoading: false,
      dataArray: CITY_NAMES
    }
  }
  loadData(refreshing) {
    if (refreshing) {
      this.setState({
        isLoading: true,
      })
    }

    setTimeout(() => {
      let dataArray = [];
      if (refreshing) {
        for (let i = this.state.dataArray.length - 1; i >= 0; i--) {
          dataArray.push(this.state.dataArray[i]);
        }
      } else {
        dataArray = this.state.dataArray.concat(CITY_NAMES)
      }

      this.setState({
        dataArray: dataArray,
        isLoading: false,
      })
    }, 2000)
  }
  _renderItem(data) {
    console.log(data)
    return <View style={styles.item}>
      <Text style={styles.text}>{data.item}</Text>
    </View>
  }
  genIndicator() {
    return <View style={styles.indicatorContainer}>
      <ActivityIndicator
        style={styles.indicator}
        size={'large'}
        color={'red'}
        animating={true}
      />
      <Text>正在加载更多</Text>
    </View>
  }
  genQuickActions() {
    return <View style={styles.quickContainer}>
      <TouchableHighlight
        onPress={() => {
          alert('确定删除？')
        }}
        >
        <View style={styles.quick}>
          <Text style={styles.text}>删除</Text>
        </View>
      </TouchableHighlight>
    </View>
  }
  render() {
    console.log(this.state.isLoading)
    return (
      <View style={styles.container}>
        <SwipeableFlatList
          data={this.state.dataArray}
          renderItem={(data) => this._renderItem(data)}
          // refreshing ={this.state.isLoading}
          // onRefresh  = {()=>{
          //   this.loadData();
          // }}
          refreshControl={
            <RefreshControl
              title={'loading'}
              colors={['red']}
              tintColor={'orange'}
              titleColor={'red'}
              refreshing={this.state.isLoading}
              onRefresh={() => {
                this.loadData(true);
              }}
            />
          }
          ListFooterComponent={() => this.genIndicator()}
          onEndReached={() => {
            this.loadData();
          }}
          renderQuickActions={() => this.genQuickActions()}
          maxSwipeDistance={100}
          bounceFirstRowOnMount = {false}
        />
      </View>
    );  
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  item: {
    backgroundColor: '#169',
    height: 100,
    marginLeft: 15,
    marginRight: 15,
    marginBottom: 15,
    alignItems: 'center',
    justifyContent: 'center'
  },
  text: {
    color: '#fff',
    fontSize: 20,

  },
  indicatorContainer: {
    alignItems: 'center'
  },
  indicator: {
    color: 'red',
    margin: 10,
  },
  quickContainer: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'flex-end',
    marginRight: 15,
    marginBottom: 15,
  },
  quick: {
    backgroundColor: 'red',
    flex: 1,
    alignItems: 'flex-end',
    justifyContent: 'center',
    padding: 10,
    width: 200,
  }
});


~~~
