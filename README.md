# Vector3_To_IntPtr
Convert Unity Vector3 to Int Ptr
```cs
class Test : MonoBehaviour{
      [StructLayout(LayoutKind.Sequential)]
      private struct Vector3Custom
      {
          public float x;
          public float y;
          public float z;
      }

      [DllImport("Vec3ToPtr.dll", CallingConvention = CallingConvention.Cdecl)]
      private static extern IntPtr GetVectorAddress(ref Vector3Custom vector);
      
      void start(){
          var position = transform.position;
          var vector = new() Vector3Custom { x= position.x, y= position.y, z= position.z};
          IntPtr address = GetVectorAddress(ref vector);
          Debug.Log($"X: {*(float*)address} Y: {*(float*)address+4} Z: {*(float*)address+8}");
      }
    }
    
    
```
