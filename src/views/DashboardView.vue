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
        <el-tab-pane label="Dashboard" > 
            <div class="content-box">
                <p> Dashboards </p> 
                <el-row>
                    <el-card shadow="hover" :style="{width:'350px'}" :body-style="{ padding: '0px' }">
                        <div class="grid-content grid-con-1">
                            <Goods class="grid-con-icon"/>
                            <div class="grid-cont-right">
                                <div class="grid-num">$ 536.23</div>
                                <div> Spending </div>
                            </div>
                        </div>
                    </el-card>
                
                    <el-card shadow="hover" :style="{width:'350px'}" :body-style="{ padding: '0px' }">
                        <div class="grid-content grid-con-2">
                            <Money class="grid-con-icon"/>
                            <div class="grid-cont-right">
                                <div class="grid-num">$ 1334.26</div>
                                <div> Income </div>
                            </div>
                        </div>
                    </el-card>
                </el-row>


            </div>
        </el-tab-pane>
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
        Goods,
        Money
        } from '@element-plus/icons-vue'
    import { onMounted, ref } from 'vue'

    const value1 = ref('')

    const size = ref<'default' | 'large' | 'small'>('default')

    const tabPosition = ref('left')

    interface Transaction {
        date: String,
        class: String[],
        amount: Number
    }


    const filterClass = (value: String, row: Transaction) => {
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
.content-box {
    background-color: #f0f0f0;
    padding: 10px;
}
.el-row {
  margin: 20px;
}

.grid-content {
	display: flex;
	align-items: center;
	height: 100px;
}

.grid-cont-right {
	flex: 1;
	text-align: center;
	font-size: 14px;
	color: #999;
}

.grid-num {
    font-size: 30px;
	font-weight: bold;
}

.grid-con-icon {
    width: 100px;
	height: 100px;
    padding: 30px;
	text-align: center;
	line-height: 100px;
	color: #fff;
}

.grid-con-1 .grid-con-icon {
	background: rgb(240, 210, 113);
}

.grid-con-2 .grid-con-icon {
	background: rgb(100, 213, 114);
}

.grid-con-1 .grid-num {
	color: rgb(240, 210, 113);
}

.grid-con-2 .grid-num {
	color: rgb(100, 213, 114);
}

</style>