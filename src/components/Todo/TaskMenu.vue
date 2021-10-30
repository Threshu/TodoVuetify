<template>
	<div>
	<v-menu
			bottom
			left
		>
			<template v-slot:activator="{ on, attrs }">
				<v-btn
				color="primary"
				icon
				v-bind="attrs"
				v-on="on"
				>
				<v-icon>mdi-dots-vertical</v-icon>
				</v-btn>
			</template>

			<v-list>
				<v-list-item
					v-for="(item, i) in items"
					:key="i"
					@click="handleClick(i)"
				>
					<v-list-item-icon>
						<v-icon v-text="item.icon"></v-icon>
					</v-list-item-icon>
					<v-list-item-title>{{ item.title }}</v-list-item-title>
				</v-list-item>
			</v-list>
		</v-menu>
		<dialog-edit
			v-if="dialogs.edit"
			@close="dialogs.edit = false"
			:task="task"
		/>
		<dialog-due-date
			v-if="dialogs.dueDate"
			@close="dialogs.dueDate = false"
			:task="task"
		/>
		<dialog-delete
			v-if="dialogs.delete"
			@close="dialogs.delete = false"
			:task="task"
		/>
	</div>
</template>

<script>
import DialogDelete from '../Todo/Dialogs/DialogDelete.vue'
import DialogEdit from '../Todo/Dialogs/DialogEdit.vue'
import DialogDueDate from '../Todo/Dialogs/DialogDueDate.vue'

export default {
	props: ['task'],
	data: () => ({
		items: [
			{ 
				title: 'Edit',
				icon: 'mdi-pencil',
				click() {
					this.dialogs.edit = true;
				}
			},
			{ 
				title: 'Due date',
				icon: 'mdi-calendar',
				click() {
					this.dialogs.dueDate = true;
				}
			},
			{ 
				title: 'Delete',
				icon: 'mdi-delete',
				click() {
					this.dialogs.delete = true;
				}
			},
			{ 
				title: 'Sort',
				icon: 'mdi-drag-horizontal-variant',
				click() {
					if(!this.$store.state.search) {
						this.$store.commit('toggleSorting');
					} else {
						this.$store.commit('showSnackbar', 'How DARE you try to sort while searching?!')
					}
				}
			}
		],
		dialogs: {
			edit: false,
        	delete: false,
			dueDate: false
      }
	}),
	methods: {
		handleClick(index) {
			this.items[index].click.call(this)
		}
	},
	components: {
		'dialog-edit': DialogEdit,
		'dialog-delete': DialogDelete,
		'dialog-due-date': DialogDueDate
	}
}
</script>

<style>

</style>