# RecyclerView
1.四种布局模式
  垂直布局： recyclerView.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false));
  水平布局： recyclerView.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.HORIZONTAL, false));
  网格布局： recyclerView.setLayoutManager(new GridLayoutManager(this, index));
  瀑布流：   recyclerView.setLayoutManager(new StaggeredGridLayoutManager(index, StaggeredGridLayoutManager.VERTICAL));
2.点击事件：定义接口
  RecyclerViewAdapter:
    /**
     * 设置点击事件
     */
    public void setOnItemClickListener(OnItemClickListener onItemClickListener) {
        this.onItemClickListener = onItemClickListener;
    }

    /**
     * 设置长按点击事件
     */
    public void setOnItemLongClickListener(OnItemLongClickListener onItemLongClickListener) {
        this.onItemLongClickListener = onItemLongClickListener;
    }
     public interface OnItemClickListener {
        void onItemClick(View view, int position);
    }

    public interface OnItemLongClickListener {
        void onItemLongClick(View view, int position);

    }
     @Override
    public void onBindViewHolder(@NonNull final RecyclerViewAdapter.ViewHolder holder, final int position) {
        holder.mtxt.setText(list.get(position).getName());
        if (onItemClickListener != null) {
            holder.mtxt.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    int position = holder.getLayoutPosition();
                    onItemClickListener.onItemClick(holder.mtv_child, position);
                }
            });
        }

        if (onItemLongClickListener != null) {
            holder.mtxt.setOnLongClickListener(new View.OnLongClickListener() {
                @Override
                public boolean onLongClick(View view) {
                    int p = holder.getLayoutPosition();
                    onItemLongClickListener.onItemLongClick(holder.mtv_child, position);
                    return true;
                }
            });
        }
    }
