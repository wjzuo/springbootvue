<template>
  <div class="deit" style="height: available">
    <div class="crumbs">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item><i class="el-icon-date"></i> 用户管理</el-breadcrumb-item>
        <el-breadcrumb-item>用户列表</el-breadcrumb-item>
      </el-breadcrumb>
      <div style="width: 100%; height: 95px">
        <el-form style="margin-top: 18px">
          <el-date-picker v-model="currentDate" type="date" placeholder="time" style="float: left;"></el-date-picker>
          <el-button style="float: left; margin-left: 20px; margin-top: 10px; color: #3b97d1" v-on:click="search">查询</el-button>
          <el-button style="float: right; margin-right: 60px; margin-top: 10px; color: #3b97d1" v-on:click="createUserInfo">新增</el-button>
        </el-form>
      </div>
      <div class="cantainer">
        <div  v-if="userData.length > 0">
          <el-table :data="userData"
                    max-height="500"
                    style="width: 100%; margin-top: -10px">
            <el-table-column fixed width="100px" prop="id">
              <template slot="header" slot-scope="scope">
                <el-tooltip content="编号" placement="top">
                  <div class="tb-header">编号</div>
                </el-tooltip>
              </template>
            </el-table-column>
            <el-table-column fixed width="160px" prop="username">
              <template slot="header" slot-scope="scope">
                <el-tooltip content="姓名" placement="top">
                  <div class="tb-header">姓名</div>
                </el-tooltip>
              </template>
            </el-table-column>
            <el-table-column width="260px" prop="address">
              <template slot="header" slot-scope="scope">
                <el-tooltip content="地址" placement="top">
                  <div class="tb-header">地址</div>
                </el-tooltip>
              </template>
            </el-table-column>
            <el-table-column width="270px"
                             prop="createDate"
                             :formatter="this.$paseDate">
              <template slot="header" slot-scope="scope">
                <el-tooltip content="消费时间" placement="top">
                  <div class="tb-header">创建时间</div>
                </el-tooltip>
              </template>
            </el-table-column>
            <el-table-column width="270px"
                             prop="modifyDate"
                             :formatter="this.$paseDate">
              <template slot="header" slot-scope="scope">
                <el-tooltip content="记录时间" placement="top">
                  <div class="tb-header">修改时间</div>
                </el-tooltip>
              </template>
            </el-table-column>
            <el-table-column fixed="right" width="180px" label="操作">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
                <el-button
                  size="mini"
                  type="danger"
                  @click="handleDelete(scope.$index, scope.row)">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
          <div>
            <el-pagination background layout="sizes, prev, pager, next" :total="totalElement"
                           @size-change="sizeChange"
                           @current-change="currentChange"></el-pagination>
          </div>
          <el-dialog title="新增用户"
                     :visible.sync="dialogVisible"
                     width="20%"
                     :modal="true"
                     :append-to-body="true"
                     :close-on-click-modal="false">
            <el-form ref="form" :model="form" label-width="80px">
              <el-form-item label="姓名">
                <el-input v-model="form.name"></el-input>
              </el-form-item>
              <el-form-item label="地址">
                <el-input v-model="form.address"></el-input>
              </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
              <el-button @click="dialogVisible = false">取 消</el-button>
              <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
            </span>
          </el-dialog>
        </div>
        <div  v-else style="text-align: center; width: 100%;">
          <span>暂无数据</span>
        </div>
      </div>
    </div>
  </div>
</template>


<script src="./userList.js"></script>

<style lang="scss" scoped>
  @import "./userList";
</style>
