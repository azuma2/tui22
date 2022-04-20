
<template>
<div class="waku">
  <div class="tes">
  <FooSidebar></FooSidebar>
  </div>
  <div class="container">
    <div class="card">
      <h1 class="title">ホーム2</h1>
            <div class="tui2">





          <div class="narabe">
        <table>
            @csrf

          
                    <tr>
            @foreach ($items as $item)
            <td>

<p class="comment">{{$item->name}}</p>
            </td>



            <form action="/tui2/update" method="post">
              @csrf
              
              <td>
                <p class="name"></p>
                <img class="icon" src="/../img/heart.png">
              </td>
                          <td>
                            </form>
              <form action="/tui2/delete" method="post" >
                    @csrf
                <input  type="hidden" name="id" value="{{$item->id}}" >
                <input class="button" type="submit" value="" >
              </form>
            </td>
            <td>
              <a href="{{ url('/') }}"><img class="icon" src="/../img/feather.png"></a>
            </td>
              <td>
                 
                <p class="comment">{{$item->content}}</p>
              </td>
            

            
          </tr>
          @endforeach
          
<tr>
  <td colspan="5">
    <p class="daiji">コメント</p>
  </td>
</tr>



              @if ($errors->has('content2'))
                  <tr>
                    <th>ERROR</th>
                  <td>
                  {{$errors->first('content2')}} 
                </td>
            </tr>
          @endif


<tr>
  @foreach ($comments as $item)
  <td colspan="5">
<p class="comment">ゲスト</p>
    <p class="comment">{{$item->content2}}</p>
  </td>
</tr>
@endforeach





<tr>
  <td colspan="5">
        <form action="/tui2/create2" method="post">
            @csrf
            <input type="text" class="area2" name="name2" />
          <input type="text" class="area2" name="content2" />
          <input class="btn" type="submit" value="追加" />
        </form>
  </td>
</tr>




                  </table>
</div>
      </div>
    </div>
    
  </div>
  
  </div>
</div>
  
</template>
