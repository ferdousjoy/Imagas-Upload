public function OurServiceDetailinsert(Request $request)
{
  if($request->hasFile('all_img')){
   $product_image=$request->file('all_img');
   $filename= str_random(5).'.'.$product_image->getClientOriginalExtension();
   Image::make($product_image)->resize(500, 400)->save(base_path('public/all_img/'.$filename),100);

 for($i=0; $i<count($request->list)-1; $i++){
    OurServiceDetail::insert([
     'title'=>$request->title,
     'text'=>$request->text,
     'list'=>$request->list[$i],
     'all_img'=>'all_img/'.$filename,
     'created_at'=>Carbon::now(),
   ]);
 }
   return back()->with('success','Data Insert Successfully');
  }
  else{
  for($i=0; $i<count($request->list)-1; $i++){
    OurServiceDetail::insert([
      'title'=>$request->title,
      'text'=>$request->text,
      'list'=>$request->list[$i],
     'all_img'=>'all_img/default.png',
   ]);
 }
      return back()->with('success','Data Insert Successfully');
  }
}
