~~~
import React, { Component } from 'react';
import {
  Platform,
  StyleSheet, // 样式绑定
  Text,
  View,
  SectionList, // list菜单
  RefreshControl, // 下拉刷新控制
  ActivityIndicator, //  loading
} from 'react-native';

type Props = {};
const CITY_NAMES = [{
  title:"一线",
  data: ['北京', '河南省', '安徽省',]
}, {
  title:"二线",
  data: ['福建省', '甘肃省', '贵州省', '海南省', '河北省', '黑龙江省', '湖北省',]
}, {
  title:"三线",
  data: ['北京', '河南省', '安徽省',]
}, {
  title:"四线",
  data: ['湖南省', '吉林省', '江苏省', '江西省', '辽宁省', '青海省', '山东省', '山西省', '陕西省',]
}, {
  title:"五线",
  data: ['四川省', '云南省', '浙江省', '台湾省', '广东省',]
}]
export default class SectionListDome extends Component<Props> {
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
  _renderSectionHeader({section}){
    return <View style={styles.sectionHeader}>
      <Text>{section.title}</Text>
    </View>
  }
  render() {
    console.log(this.state.isLoading)
    return (
      <View style={styles.container}>
        <SectionList
          sections={this.state.dataArray}
          renderItem={(data) => this._renderItem(data)}
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
          renderSectionHeader={(data)=>this._renderSectionHeader(data)}
          ItemSeparatorComponent={()=><View style={styles.separator}  />}
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
    height: 80,
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
  sectionHeader: {
    height: 50,
    backgroundColor: '#999',
    alignItems:'center',
    justifyContent: 'center',
  },
  separator:  {
    height: 1,
    backgroundColor:'gray',
    flex: 1,
  }
});


~~~
