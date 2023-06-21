<template>
    <el-tabs :tab-position="tabPosition" class="demo-tabs">
        <el-tab-pane label="Transactions"> 
            <el-row>
                <el-date-picker
                    v-model="value1"
                    type="daterange"
                    range-separator="To"
                    start-placeholder="Start date"
                    end-placeholder="End date"
                    :size="size"
                />
            </el-row>
            

            <el-table :data="tableData" stripe height="250" style="width: 100%">
                <el-table-column prop="date" label="Date" sortable width="160" />
                <el-table-column prop="class" label="Class" width="160" 
                    :filters="[
                        { text: 'Grocery', value: 'Grocery'},
                        { text: 'Bill', value: 'Bill'},
                        { text: 'Entertainment', value: 'Entertainment'},
                    ]" 
                    :filter-method="filterClass"
                >
                    <template #default="scope">
                        <el-tag v-for="item in scope.row.class">{{ item }}</el-tag>
                    </template>
                </el-table-column>
                <el-table-column prop="amount" label="Amount" sortable width="160" />
            </el-table>
            <el-row>
                <el-button type="primary">Primary</el-button>
                <el-button type="success" :icon="Check" circle />
                <el-button type="info" :icon="Message" circle />
                <el-button type="warning" :icon="Star" circle />
                <el-button type="danger" :icon="Delete" circle />
            </el-row>
        </el-tab-pane>
        <el-tab-pane label="Dashboard"> Dashboards </el-tab-pane>
        <el-tab-pane label="Management"> Management </el-tab-pane>
    </el-tabs>
</template>

<script lang="ts" setup>
    import {
        Check,
        Delete,
        Edit,
        Message,
        Search,
        Star,
        } from '@element-plus/icons-vue'
    import { ref } from 'vue'
    import type { TableColumnCtx, TableInstance } from 'element-plus'
    import { ca } from 'element-plus/es/locale/index.js';
import type { Table } from 'element-plus/es/components/index.js';
    
    const tabPosition = ref('left')

    interface Transaction {
        date: String,
        class: String[],
        amount: Number
    }

    const tableRef = ref<TableInstance>()

    const filterClass = (value: String, row: Transaction, column: TableColumnCtx<Transaction>) => {
        return row.class.includes(value)
    }

    const tableData: Transaction[] = [
        {
            date: '2023-05-03',
            class: ['Grocery', 'Cloth'],
            amount: 20.00
        },
        {
            date: '2023-05-04',
            class: ['Bill', 'Electricity'],
            amount: 69.54
        },
        {
            date: '2023-05-06',
            class: ['Entertainment'],
            amount: 23.44
        },
    ]
</script>

<style>
.el-row {
  margin: 20px;
}
</style>